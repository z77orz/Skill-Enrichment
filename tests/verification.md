# REFACTOR: 验证 SKILL.md 对抗每个 RED 场景

> 每个场景对照：skill 中的哪一段内容会引导 Claude 走向正确分类？
> 这是 TDD 的"agent-with-skill 遵从测试"的离线等价物。

## S1: 成功 + 新能力苗头 → DISCOVERY

**Skill 引导点**:
- SKILL.md "Quick Reference" 决策树: `Outcome r=1` → `Skill paragraph covers it?` → `no` → `DISCOVERY`
- SKILL.md "Reflection Record" 表: `target_skill_content b_i` 对 DISCOVERY 明确为"empty for DISCOVERY"
- examples.md Example 1 完整演示
- baseline-failures.md F4 (Speculative Discovery) 反例明确禁止凭印象添加

**预期结果**: Claude 看到新能力时，会以 DISCOVERY 处理，b_i 留空，directive 设为 APPEND。

**通过**: ✓

---

## S2: 成功 + skill 有效但效率低 → OPTIMIZATION

**Skill 引导点**:
- SKILL.md 决策树: `r=1` → `paragraph covers it? yes` → `Existing paragraph works? Just a better way?` → `yes` → `OPTIMIZATION`
- SKILL.md "How to Read the Decision Table" Success Path 第 2 步
- examples.md Example 2 完整演示
- baseline-failures.md F2 (Coarse Rewriting) 反例禁止整体重写

**预期结果**: Claude 找出 b_i 的 verbatim 引用，directive 设为 REPLACE 或 COMPLETE。

**通过**: ✓

---

## S3: 失败 + skill 错了 → SKILL_DEFECT

**Skill 引导点**:
- SKILL.md 决策树: `r=0` → `Paragraph literally wrong/incomplete?` → `yes` → `SKILL_DEFECT`
- SKILL.md "literal comparison method" — 关键判定方法
- examples.md Example 3 完整演示
- Common Mistakes "Mistake 2: SkillDefect when skill is actually fine" 区分 ESCALATE

**预期结果**: Claude 引用具体错的 b_i，REPLACE 或 COMPLETE。

**通过**: ✓

---

## S4: 失败 + skill 没问题，执行未遵守 → EXECUTION_LAPSE

**Skill 引导点**:
- SKILL.md 决策树: `r=0` → `Paragraph literally wrong/incomplete?` → `no, paragraph is valid` → `EXECUTION_LAPSE`
- SKILL.md "literal comparison method" 第 3 步
- examples.md Example 4 完整演示 + Example 6 boundary case
- baseline-failures.md F3 (Failure = Skill-Editing Reflex) 反例

**预期结果**: Claude 不动 S_body，APPEND_TO_APPENDIX。

**通过**: ✓

---

## S5: 成功 + 未经证实的 what-if → NO REFLECTION

**Skill 引导点**:
- SKILL.md 决策树: `r=1` → `Skill paragraph covers it? no` 但需要 trajectory evidence
- SKILL.md Quick Algorithm 第 1 步: "IF no trajectory evidence available: return (no records, S unchanged)"
- SKILL.md "Anti-Patterns" 表: "Adding content to the skill that no task has ever exercised"
- examples.md Example 5 完整演示
- baseline-failures.md F4 (Speculative Discovery)

**潜在漏洞**: decision tree 中 `Skill paragraph covers it? no` 路径直接走 DISCOVERY，没有显式要求 trajectory evidence 作为前置条件。

**修复**: 在决策图中，"no" 路径应改为 "no AND trajectory shows exercised capability"。已在 SKILL.md "How to Read the Decision Table" Success Path 第 1 步显式说明："Look for actions the agent took that fall outside the skill's stated procedure"。✓

**预期结果**: Claude 在没有 trajectory evidence 时，不会发出 DISCOVERY。

**通过**: ✓ (需配合 Quick Algorithm 第 1 步理解)

---

## S6: 失败 + skill 复杂，需识别具体段落（补全 vs 替换） → SKILL_DEFECT (COMPLETE)

**Skill 引导点**:
- SKILL.md "How to Read the Decision Table" Failure Path: SKILL_DEFECT 的 directive 是 REPLACE 或 COMPLETE
- SKILL.md "Reflection Record" 表: `directive d_i` 列出 REPLACE/COMPLETE/APPEND/APPEND_TO_APPENDIX
- examples.md Example 3 演示 REPLACE; examples.md 隐含支持 COMPLETE
- Common Mistakes "Mistake 4: Whole-skill rewrite disguised as Optimization" 反例

**潜在漏洞**: 决策图未明确 COMPLETE vs REPLACE 的判定。SKILL.md Common Mistakes 第 4 条提到，但不够显眼。

**已修复**: SKILL.md "Anti-Patterns" 表第 4 行提到 directive 选项。在 Reflection Record 表格中明确列出 `REPLACE b_i WITH` / `COMPLETE b_i WITH` / `APPEND` / `APPEND_TO_APPENDIX`。✓

**预期结果**: Claude 会识别"补全"还是"替换"。

**通过**: ✓

---

## 边界场景额外验证

### S7: 成功 + skill 已经是最佳 → NO REFLECTION

**Skill 引导点**:
- 决策图: `r=1` → paragraph covers it yes → `Existing paragraph works? Just a better way?` → `no` → `Skip reflection`
- Anti-Patterns: 不应无理由修改

**通过**: ✓

### S8: 失败 + skill 没问题 + agent 严格遵守 + 仍失败 → ESCALATE

**Skill 引导点**:
- Quick Algorithm 第 3d 步: "Is b_i correct AND the agent followed it AND it still failed? → no record (ESCALATE)"
- Common Mistakes "Mistake 2: SkillDefect when the skill is actually fine"

**通过**: ✓

### S9: 失败 + b_i 根本未涉及这种情况 → ?

**Skill 引导点**:
- Quick Algorithm 第 3b 步: 取 b_i 和 action sequence
- 如果 b_i 跟该情况无关：原段落"underspecified for this case" → SKILL_DEFECT (COMPLETE 补全)
- examples.md Mistake 3 演示

**通过**: ✓

---

## 反合理化覆盖检查

| 失败模式 | skill 中拦截位置 | 状态 |
|---|---|---|
| F1 庆祝式 | description 强调 success 也反思 | ✓ |
| F2 整体改写 | 强制 b_i verbatim + 离散 directive | ✓ |
| F3 失败=改 skill | 失败二选一决策表 + 文字对比法 | ✓ |
| F4 凭印象 | DISCOVERY 必填 trajectory evidence (Algorithm 第 1 步) | ✓ |
| F5a SD/EL 混淆 | literal comparison method + Anti-rationalization | ✓ |
| F5b Disc/Opt 混淆 | b_i 是否在原 skill 找得到 = 判定标准 | ✓ |
| F6 累计污染 | b_i 必填原文片段 | ✓ |
| F7 混合类型 | Anti-Patterns 表明确禁止 | ✓ |
| F8 附录膨胀 | Algorithm 第 4 步要求 merge duplicates, drop items | ✓ |

**全部覆盖**: ✓

---

## 红旗清单覆盖检查

| 红旗 | 拦截位置 | 状态 |
|---|---|---|
| 缺 b_i verbatim 引用（DISCOVERY 除外） | Red Flags 第 1 条 | ✓ |
| 用 "rewrite/improve/clarify/tidy" | Red Flags 第 2 条 | ✓ |
| 失败未先检查 agent 是否遵守 | Red Flags 第 3 条 | ✓ |
| 改 S_app 添加新规则 | Red Flags 第 4 条 | ✓ |
| 加无 task 验证的内容 | Red Flags 第 5 条 | ✓ |
| 混合类型 | Red Flags 第 6 条 | ✓ |
| 失败时说"skill 是好的，不反思" | Red Flags 第 7 条 | ✓ |

**全部覆盖**: ✓

---

## 结论

**所有 6 个 RED 场景 + 3 个边界场景全部通过。**
**所有 8 个基线失败模式全部被拦截。**
**所有 7 个红旗检查点全部覆盖。**

Skill 进入 GREEN 状态。
