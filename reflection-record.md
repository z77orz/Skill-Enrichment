# Reflection Record 模板

> 复制以下模板到你的笔记/记忆/会话记录中。每次任务结束后填一份。

## 模板

```markdown
# Reflection Record — <date> <task short name>

## 1. 任务元信息
- **任务**:
- **使用的 skill / 流程**:
- **结果 r**: 0 (失败) / 1 (成功)
- **轨迹证据来源**: (会话日志 / 工具调用历史 / 测试输出)

## 2. 四类判定
- [ ] r=1 + 新能力未被 skill 覆盖  → **DISCOVERY**
- [ ] r=1 + 现有段落可优化       → **OPTIMIZATION**
- [ ] r=1 + skill 已是最佳        → NONE
- [ ] r=0 + skill 字面错误/缺失  → **SKILL_DEFECT**
- [ ] r=0 + skill 正确但 agent 未遵守 → **EXECUTION_LAPSE**
- [ ] r=0 + skill 正确 + agent 已遵守 + 仍失败 → ESCALATE

(勾选最匹配的一项)

## 3. 记录

```text
[REFLECTION: <TYPE>]
evidence:
  - "<quote 1 from trajectory>"
  - "<quote 2 from trajectory>"
target_skill_content b_i: |
  "<verbatim quote of the targeted paragraph in S_body>"
  (or empty for DISCOVERY)
directive: <REPLACE b_i WITH | COMPLETE b_i WITH | APPEND | APPEND_TO_APPENDIX>
new_content:
  <the new / replacement / addendum / appendix reminder text>
```

## 4. 自检
- [ ] b_i 是从 S_body 原文 verbatim 引用（DISCOVERY 除外）
- [ ] 只有一个 type
- [ ] evidence 来自实际轨迹，不是假设
- [ ] 对成功路径: 移除这条记录会改变 skill 吗？若不会，不应发
- [ ] 对失败路径: 完美 agent 严格按 skill 执行会成功吗？
  - 是 → SKILL_DEFECT 错（应为 EXECUTION_LAPSE）
  - 否，但 skill 正确 → EXECUTION_LAPSE
  - skill 也错 → SKILL_DEFECT ✓

## 5. 更新后 S
（在此粘贴更新后的 S_body 和 S_app）
```

---

## 5 种常见填写错误

| 错误 | 后果 | 修复 |
|---|---|---|
| evidence 用"可能是因为…"推测 | 反射基于猜测 | 改为引用实际工具调用或日志 |
| b_i 用自己的话改写 | 修改漂移 | 必须从 skill 原文复制粘贴 |
| 把 ExecutionLapse 的 evidence 写成"skill 没说清楚" | 把执行错误归到 skill | 改为"skill 说了 X，agent 做了 Y" |
| 把 Discovery 的 b_i 留空后又填了一段旧 skill 的引用 | 类型不一致 | Discovery 的 b_i 必须完全留空 |
| directive 写成"完善/改进/优化整段" | 触发整体改写 | 改用 REPLACE / COMPLETE / APPEND |

---

## 与其他工具的集成建议

- **Obsidian**: 把 reflection record 存到 `Reflection/<date>-<task>.md`，每条记录链接到被修改的 skill 路径。
- **Claude Memory**: 在长期记忆中保留"上次反思的教训"，下次同类任务时主动检查。
- **Skill 仓库**: 每次修改 skill 前先填记录 → 修改 → 记录里的"更新后 S"与实际 skill diff 验证一致性。
