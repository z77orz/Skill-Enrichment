# Skill-Enrichment PRD — 用户主动触发版

> 本文档定义 v2 版本的 Skill-Enrichment:从"被动事后反思"改为"用户主动触发+多任务列表+确认后再改"。

## Problem Statement

### 现状(诊断数据)

| 维度 | 数据 |
|---|---|
| 触发模式 | 被动:任务自动完成时,skill 主动判断是否反思 |
| 触发召回 | **0%**(5 轮 trigger eval 全部 0% recall) |
| 反思范围 | 单一任务、单一 skill(无聚合能力) |
| 修改方式 | 即时直接修改 SKILL.md(不可逆) |

### 核心问题

1. **触发不可靠**:Claude 看到 query 后觉得自己"能直接反思",不去查 skill 文件——`claude -p` 的 0% recall 证明自动触发机制结构性失效
2. **范围太窄**:用户视角下,"我今天用了 5 个 skill,有些跑得好有些不好,想整体复盘"——但当前 skill 一次只能反思一个
3. **不可逆修改**:直接 Edit skill 文件,无 review 机会,改错就污染 skill
4. **错过跨 skill 模式**:同一次会话里多次用 `contract-review`,第一次有缺陷,第二次绕过——skill 看不出来"同一个 skill 反复出问题"

### 谁受影响

| 角色 | 痛点 |
|---|---|
| Skill 作者 | 想批量观察"用户怎么用我的 skill",但当前只能被动等单次反思 |
| 高级用户(Claude Code power user) | 一次会话里跑过 10 个 skill,想下班前整体盘点 |
| 多 skill 流水线使用者 | 想看"我那 5 次 `iterative-retrieval` 调用中哪几次有 improvisation" |

### 不解决的后果

- skill 永远不会变好——因为触发率 0%,从来没有过 reflection record
- 用户的"事后复盘"需求被忽略,只能靠记忆
- 同一 skill 的反复缺陷被掩盖(每次任务独立,看不到 cross-task 模式)

---

## Goals

| # | Goal | 可度量 |
|---|---|---|
| G1 | 用户说"反思技能"/"进化技能"/"优化技能"时,**100% 触发**(手动语义) | 任何包含触发词的中文 query → skill 加载 |
| G2 | 列出当前会话已执行的所有任务 + 涉及的 skill,让用户挑选 | 列表完整性 ≥ 95%(漏掉的任务用户能补) |
| G3 | 选定组合后先生成 reflection record,用户确认后才改文件 | 100% 改文件前必须确认(无直接 Edit) |
| G4 | 支持同一 skill 的多次执行聚合(用户选"聚合"模式时) | 输出按 skill 合并的 record 列表 |
| G5 | 反思记录可追溯、可回滚 | 每条 record 含时间戳、任务 ID、变更前 b_i 快照 |

---

## Non-Goals

| # | Non-Goal | 原因 |
|---|---|---|
| NG1 | 自动任务完成时触发 | 已被验证结构性失败(0% recall),不在 v2 范围 |
| NG2 | 跨会话持续追踪 | v2 只看"当前会话",跨会话需要持久化层(后续版本) |
| NG3 | 反思非 Claude Code 任务 | v2 只针对 Claude Code 会话里的 skill 使用 |
| NG4 | 反思中实际"自动生成 new_content 草案" | v2 只让 skill 标记"需要补什么",具体草稿用户写或后续 roundtrip |
| NG5 | 反思过程中调用 LLM 自动分类 | v2 用户主导分类,LLM 只做证据抽取与组织 |

---

## User Stories

### 角色定义

| 角色 | 描述 |
|---|---|
| **Skill Author** | 写 skill 的人,想知道 skill 在实战中哪里有问题 |
| **Power User** | 一会话跑多个 skill 的高级用户,想下班前整体复盘 |
| **Pipeline User** | 多步流水线中使用同一 skill 多次的人 |

### P0 — 必须有

| ID | Story |
|---|---|
| US-1 | As a Power User, **当我说"反思技能"时**, skill 立即列出本次会话所有已执行任务+涉及 skill,让我挑选。 |
| US-2 | As a Power User, **当我说"进化技能"或"优化技能"时**, 行为与"反思技能"完全一致(同义触发词)。 |
| US-3 | As a Skill Author, **当我挑选了 (任务 A, skill X) 组合时**, skill 输出一份 reflection record(包含 [REFLECTION: TYPE] / evidence / b_i / directive / new_content 五段),**不直接修改文件**,等我确认。 |
| US-4 | As a Power User, **当我确认了 record 后**, skill 才执行 Edit/Write 真正修改 SKILL.md。 |
| US-5 | As a Power User, **如果我拒绝 record**, skill 不修改文件,记录保留为"未采纳"以便回看。 |
| US-6 | As a Pipeline User, **当我对同一 skill 选多次任务时**, skill 让我选"逐个反思"或"聚合反思";聚合模式下输出按 skill 合并的 record 集。 |

### P1 — 应该有

| ID | Story |
|---|---|
| US-7 | As a Skill Author, **反思完成后**, skill 把 record 写到本地 `~/.claude/skills/Skill-Enrichment/reflections/YYYY-MM-DD.md`,作为审计日志。 |
| US-8 | As a Power User, **在列表任务时**, 我能看到每个任务的简短摘要(头一句话)+耗时+结果(success/partial/fail)。 |
| US-9 | As a Skill Author, **多次跑同一 skill 时**, skill 提示"该 skill 在本次会话被使用 N 次,其中 M 次触发 reflection",帮用户判断要不要聚合。 |

### P2 — 未来考虑

| ID | Story |
|---|---|
| US-10 | As a Power User, **跨会话复盘时**, skill 能从 SQLite 读历史 reflection,做"上周 X skill 被标记 3 次 SkillDefect"的趋势分析。 |
| US-11 | As a Skill Author, **b_i 修改后**, skill 自动跑 trigger eval,验证 description 没被改坏。 |
| US-12 | As a Pipeline User, **我想回滚某次反思时**, skill 根据反射日志的 b_i 快照,自动生成 `git diff -R` 命令。 |

---

## Requirements

### Must-Have (P0)

#### REQ-1: 触发词检测

**描述**:当用户 query 包含以下任一触发词时,skill 必须立即加载并启动流程。

| 触发词类别 | 中文 |
|---|---|
| 主触发词 | 反思技能、进化技能、优化技能 |
| 衍生触发词(同义) | 复盘技能、丰容技能、技能复盘 |
| 英文(可选) | reflect on skill, evolve skill, optimize skill |

**Acceptance Criteria**:
- [ ] 用户说"帮我反思技能"→ 立即触发(不等其他条件)
- [ ] 用户说"今天用了好多 skill,进化一下"→ 触发
- [ ] 用户说"刚才 contract-review 跑得慢,反思一下"→ 触发
- [ ] 触发词**不**在代码块/字符串字面值内时,不误触发

#### REQ-2: 任务+skill 列表生成

**描述**:skill 必须能从当前会话上下文中提取"已执行的任务"和"涉及的 skill"。

| 字段 | 数据源(候选) | 优先级 |
|---|---|---|
| 任务标题/摘要 | 会话消息(Read 工具读 transcript) | P0 |
| 任务耗时 | 任务开始/结束时间戳 | P1 |
| 任务结果 | success/partial/fail 标签(用户/agent 标记) | P1 |
| 涉及的 skill | 任务描述中引用的 skill 名(`` `xxx-skill` ``) | P0 |
| 涉及的 sub-skill | 同上(嵌套) | P1 |

**Acceptance Criteria**:
- [ ] 列表按时间顺序呈现
- [ ] 每个条目包含:序号、任务摘要(≤ 30 字)、涉及 skill 列表、结果(若可知)
- [ ] 如果任务数 = 0,提示"当前会话无任务可反思"
- [ ] 如果任务数 > 20,提示用户筛选"全部 / 最近 5 / 指定范围"

#### REQ-3: 用户挑选交互

**描述**:用 `AskUserQuestion`(多选)让用户挑 (任务, skill) 组合。

**Acceptance Criteria**:
- [ ] 展示格式:`任务 #N: <摘要> | skill: <X>, <Y>`
- [ ] 用户多选(可一次选多组)
- [ ] 用户选完后,如果选了同一 skill 多次,询问"逐个 / 聚合"

#### REQ-4: Reflection Record 生成

**描述**:按 EmbodiSkill 四类框架(Discovery/Optimization/SkillDefect/ExecutionLapse)产出 reflection record。

**格式(必填)**:
```
[REFLECTION: <TYPE>]
evidence: <从任务轨迹摘录的 1-3 行>
target_skill_content b_i: <SKILL.md 中某段的 verbatim 引用>
directive: <REPLACE b_i WITH | COMPLETE b_i WITH | APPEND | APPEND_TO_APPENDIX>
new_content: <替换/补全内容>
```

**Acceptance Criteria**:
- [ ] b_i 必须是 SKILL.md 的 verbatim 引用(用 Grep 验证)
- [ ] directive 必须是四个枚举值之一(用枚举校验)
- [ ] evidence 必须来自实际任务(用"hypothetical"/"imagine"等关键词检测并拒绝)
- [ ] 同一类型多组任务时(聚合模式),输出多条 record 共享同一 SKILL.md 章节

#### REQ-5: 用户确认机制

**描述**:record 草稿生成后,**必须**等待用户确认才能改文件。

**Acceptance Criteria**:
- [ ] 用 `AskUserQuestion` 提供选项:`采纳 / 拒绝 / 修改后采纳`
- [ ] 用户拒绝 → 记录到 reflections log 标"rejected",**不**改文件
- [ ] 用户采纳 → 执行 Edit/Write,把 b_i 替换为 new_content
- [ ] 用户"修改后采纳" → 收集修改意见,重新生成 record 再走流程

#### REQ-6: 修改前的安全检查

**描述**:对每个待改的 SKILL.md,在 Edit 前做 sanity check。

**Acceptance Criteria**:
- [ ] b_i 字符串在 SKILL.md 中**唯一**匹配(用 `grep -c` 验证)
- [ ] 改后 SKILL.md 行数变化 ≤ 50%(防"全文重写"反模式)
- [ ] 若验证失败,提示用户手动定位,而不是模糊匹配

### Should-Have (P1)

#### REQ-7: 审计日志

每次 reflection(无论采纳与否)写入 `~/.claude/skills/Skill-Enrichment/reflections/YYYY-MM-DD.md`。
格式见 [README.zh.md - 审计日志格式](#)。

#### REQ-8: 任务摘要自动生成

任务摘要若会话上下文无现成标题,LLM 生成 ≤ 30 字摘要,用户可编辑。

#### REQ-9: 同 skill 多次提示

当用户选了同一 skill 的 ≥ 2 个任务,主动提示聚合选项。

### Future (P2)

#### REQ-10: 跨会话趋势

需要持久化层(未规划)。

#### REQ-11: 改后回归

`description` 改动后自动跑 trigger eval。

#### REQ-12: 一键回滚

从反射日志生成 `git diff -R` 命令。

---

## End-to-End UX 流程(ASCII)

```
用户 query 包含触发词
    │
    ▼
[1] 解析触发:skill 加载
    │
    ▼
[2] 扫描会话 → 提取 (任务, skill) 列表
    │
    ▼
[3] AskUserQuestion(多选): "请挑要反思的组合"
    │
    ▼
[4] 同一 skill 被选 ≥2 次? ──→ 是 ──→ AskUserQuestion: "逐个/聚合"
    │                                  │
    │                                  ▼
    │                            聚合 / 逐个模式
    │                                  │
    ◀──────────────────────────────────┘
    │
    ▼
[5] 对每个组合生成 reflection record 草稿
    │
    ▼
[6] AskUserQuestion(单选): "采纳 / 拒绝 / 修改后采纳"
    │
    ├─ 拒绝 → 写日志(rejected) ──→ 继续下一组合
    ├─ 修改 → 收集意见重生成 ──→ 回到 [5]
    └─ 采纳 → Sanity check(b_i 唯一 / 行数变化)
                │
                ├─ 失败 → 提示用户手动定位
                └─ 通过 → Edit SKILL.md
                          │
                          ▼
                     写日志(accepted)
                          │
                          ▼
                     继续下一组合
                          │
                          ▼
                  [全部完成] 总结报告
```

---

## Acceptance Criteria 汇总(总清单)

| # | Criterion | 验证方式 |
|---|---|---|
| AC-1 | 包含 3 个主触发词(反思/进化/优化 技能)任一 → 100% 触发 | trigger eval |
| AC-2 | 列表阶段展示当前会话所有已执行任务+涉及 skill | 单元测试 + 手动 |
| AC-3 | 用户多选后,聚合模式产出合并 record;逐个模式产出独立 record | 端到端测试 |
| AC-4 | 任何改文件前,必须经 AskUserQuestion 确认 | 代码 review + 集成测试 |
| AC-5 | b_i 必须是 SKILL.md verbatim 唯一匹配 | 自动化断言 |
| AC-6 | 改后行数变化 ≤ 50% | pre/post diff 检查 |
| AC-7 | 每次 reflection 写日志,含 record + 接受状态 | 文件存在性 + 内容检查 |
| AC-8 | should-not-trigger case(改 SKILL.md、写代码等)不误触发 | trigger eval |

---

## Open Questions

| # | Question | 阻塞? | 解答方 |
|---|---|---|---|
| Q1 | 触发词是否要支持英文?`reflect on skill` 之类 | 否 | 用户后续决定 |
| Q2 | 审计日志的 retention?(保留多久) | 否 | 用户决定 |
| Q3 | 跨会话趋势(US-10)的存储选型(SQLite / JSONL / 其他)? | 否 | v3 决定 |
| Q4 | "修改后采纳"模式是文本框还是结构化字段? | 否 | UX 迭代时定 |
| Q5 | 如果 SKILL.md 是 git tracked 的,改完是否自动 commit? | 否 | 用户后续决定 |

---

## Timeline & Phasing

| 阶段 | 交付 | 预计 |
|---|---|---|
| **v2.0 — MVP** | REQ-1, 2, 3, 4, 5, 6(P0 全集) | 单次开发 |
| **v2.1** | REQ-7(审计日志)+ REQ-8(摘要生成) | v2.0 后 1 周 |
| **v2.2** | REQ-9(同 skill 聚合提示优化) | v2.1 后 |
| **v3.0** | REQ-10/11/12(跨会话+回归+回滚) | 视需要 |

---

## 关联文档

| 文档 | 用途 |
|---|---|
| [SKILL.md](./SKILL.md) | 当前版本(将被本 spec 替换) |
| [README.zh.md](./README.zh.md) | 项目介绍(需同步更新触发说明) |
| [evals/evals.json](./evals/evals.json) | trigger eval 集(需按本 spec 重写) |
| [examples.md](./examples.md) | 6 个反思案例(可作为 v2 的基础,但需追加"用户主动触发"的新 example) |

---

## 文档元信息

| 字段 | 值 |
|---|---|
| Spec 名称 | Skill-Enrichment 用户主动触发版 |
| Spec 版本 | v2.0-draft |
| 撰写日期 | 2026-06-03 |
| 撰写者 | Claude (with skill-creator workflow) |
| 关联论文 | EmbodiSkill (Ju et al., 2026, arXiv:2605.10332) |
| 上一版本诊断 | 5 轮 trigger eval,recall 0%(自动触发结构性失效) |
