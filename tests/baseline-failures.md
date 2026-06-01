# RED: 基线失败模式（无 skill 时 Claude 怎么做错）

> 本文件记录"无 skill 时 Claude 在任务反思环节的典型错误"。
> 这些失败模式是 skill 必须堵住的"漏洞"。

---

## 失败模式 F1：庆祝式反射（Celebration Bias）

**触发条件**：任务成功，无论 skill 用得是否高效。

**典型行为**：
- "任务完成 ✓，很顺利。"
- "Skill 表现良好，下一次继续使用。"
- 不输出任何 reflection record。

**根因**：成功的正向反馈会触发 Claude 的"完成 → 结束"反射，关闭反思回路。

**skill 必须做的拦截**：在 description 中明确包含"success 也需要反思"；在正文中显式列出成功路径的两种反思（Discovery / Optimization），不让成功直接走"结束"分支。

---

## 失败模式 F2：整体改写（Coarse Rewriting）

**触发条件**：任何反思信号出现。

**典型行为**：
- "重写一下 skill，让它更完善……"
- 把整个 skill 用 LLM 重生成，丢失原 skill 的特定表达和细节。
- 把"部分修改"扩大为"全篇润色"。

**根因**：Claude 倾向于把"修改"理解为"生成新版本"，而不是"在原文上做最小编辑"。

**skill 必须做的拦截**：强制要求 reflection record 包含 `target_skill_content b_i`（具体段落引用）；directive d_i 必须明确是【追加】/【替换】/【补全】/【不修改】之一，不能是"重写"。

---

## 失败模式 F3：失败 = 改 skill（Failure = Skill-Editing Reflex）

**触发条件**：任务失败。

**典型行为**：
- 直接修改 skill 文字，假设 skill 错了。
- 忽略"执行未遵守"这种可能性。

**根因**：失败引发归因反射，归因对象默认是"用过的工具"而不是"自己"。

**skill 必须做的拦截**：在失败分支强制二选一决策表（"skill 错了" vs "skill 没被遵守"），并提供明确的判定方法（对比 skill 文本与实际执行轨迹的字面差异）。

---

## 失败模式 F4：凭印象添加（Speculative Discovery）

**触发条件**：成功任务中，Claude 想到"要是能 X 就更好了"。

**典型行为**：
- 把"X"作为新 skill 段落 append 进去。
- 没意识到 X 并没有被任何任务实际触发。

**根因**：Claude 倾向于把"合理的扩展"等同于"应当被记录"，混淆了"未来可能性"与"已发生能力"。

**skill 必须做的拦截**：DISCOVERY 的判定条件明确要求"轨迹证据"；没有 trajectory evidence 时直接归类为 NO REFLECTION。

---

## 失败模式 F5：边界混淆（Boundary Confusion）

最严重的失败模式之一。在四个反思类型的边界上反复犯：

### F5a: SkillDefect ↔ ExecutionLapse 混淆

| 错误分类 | 错在哪里 | 后果 |
|---|---|---|
| 把 ExecutionLapse 误判为 SkillDefect | 改 skill | skill 越来越啰嗦，原始有效内容被反复改写 |
| 把 SkillDefect 误判为 ExecutionLapse | 不改 skill | 失败的根因没修，下次还会失败 |

**关键判定**：
- 取出 skill 中相关段落的字面文本
- 取出 agent 实际执行的动作序列
- 字面一致 → ExecutionLapse
- 字面矛盾或 skill 缺失 → SkillDefect

### F5b: Discovery ↔ Optimization 混淆

| 错误分类 | 错在哪里 | 后果 |
|---|---|---|
| 把 Discovery 误判为 Optimization | 把新内容塞到旧段落里 | 旧段落语义被污染 |
| 把 Optimization 误判为 Discovery | 把可优化的旧段落作为新能力记录 | skill 越来越长，原段落得不到修复 |

**关键判定**：
- target_skill_content b_i 是否能在原 skill 中找到对应文字？
- 找到 → 优化（替换/补全 b_i）
- 找不到 → Discovery（新增 b_i 为空）

---

## 失败模式 F6：连续多次反思被覆盖（Cumulative Pollution）

**触发条件**：在同一会话中对同一 skill 多次反思。

**典型行为**：
- 第一次：合理修改。
- 第二次：在第一次修改的基础上再次"优化"，但已经失去原 skill 的关键细节。
- 第三次：skill 已面目全非。

**根因**：每次反思都缺乏"对比原 skill"的意识。

**skill 必须做的拦截**：每次 reflection record 必填 `target_skill_content b_i`（带原文片段），让修改建立在"原文字段"基础上而不是"上一版修改"上。

---

## 失败模式 F7：跨类型一锅烩（Mixed-Type Records）

**触发条件**：一次反思中包含多种类型。

**典型行为**：
- 一个 reflection record 里同时有 Discovery 和 Optimization。
- 一次"重写"既改了 skill body 又加了 appendix 内容。

**根因**：Claude 倾向于"一次性解决所有问题"。

**skill 必须做的拦截**：明确"一个 reflection record 只能属于一个类型"；如果任务同时触发多个类型，必须分多个 record 提交。

---

## 失败模式 F8：执行附录膨胀（Appendix Bloat）

**触发条件**：多次 ExecutionLapse 反思。

**典型行为**：
- 把所有"过去没遵守的"段落都堆到 S_app 里。
- S_app 越来越长，喧宾夺主。

**根因**：没有"清理过期 appendix 条目"的机制。

**skill 必须做的拦截**：S_app 的更新规则是"高亮有效段落的执行提醒"，应当 merge 重复、删除与 S_body 不再对应的项；不能让 S_app 取代 S_body 成为主信息源。

---

## 总结：skill 必须包含的 8 个拦截点

| # | 拦截的失败模式 | 拦截手段 |
|---|---|---|
| 1 | F1 庆祝式 | description 强调 success 也要反思；正文显式列成功路径 |
| 2 | F2 整体改写 | 强制 b_i + 离散 directive（追加/替换/补全/不修改） |
| 3 | F3 失败 = 改 skill | 失败二选一决策表 + 文字对比法 |
| 4 | F4 凭印象 | DISCOVERY 必填 trajectory evidence |
| 5 | F5 边界混淆 | 反合理化表 + 字面对比法 |
| 6 | F6 累计污染 | b_i 必填"原文片段"，强制对比原 skill |
| 7 | F7 混合类型 | 一 record 一类型 |
| 8 | F8 附录膨胀 | S_app 更新规则 + 合并/删除规则 |
