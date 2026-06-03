# Changelog — Skill-Enrichment

本文件记录 `description` 字段的演变历史(因为 description 是触发机制的核心,任何改动都应留底便于回溯)。

**保留对象**:`SKILL.md` YAML frontmatter 的 `description` 字段(精确字符串)。

---

## v2.0 — 2026-06-03(commit `2542963`)

**核心变更**:触发机制从"被动事后反思"改为"用户主动触发 + 列表式任务盘点 + 确认门控"。

### Description

```
Use when the user explicitly says "反思技能" / "进化技能" / "优化技能" / "复盘技能" / "丰容技能" / "技能复盘" (or English equivalents like "reflect on skill", "evolve skill", "optimize skill"). On trigger, the skill (1) scans the current session for all executed tasks and the skills they used, (2) presents a numbered list and asks the user to select (task, skill) combinations to reflect on, (3) for each selection generates a typed reflection record (Discovery / Optimization / SkillDefect / ExecutionLapse) targeting a specific `b_i` paragraph, (4) shows the record and waits for the user's explicit confirmation before editing the SKILL.md. (丰容 / Skill Enrichment — formerly Skill-Aware Reflection.)
```

### Trigger eval 数据

| 指标 | 值 |
|---|---|
| Precision | 76% |
| Recall | 39% |
| Accuracy | 60% |
| Trigger eval 集 | 20 queries(11 触发 + 9 不触发,全中文) |

### 配套变更

| 文件 | 变化 |
|---|---|
| `SKILL.md` | v1 → v2 重写(464 行 total) |
| `evals/evals.json` | 4 task evals → 20 trigger queries(146 行 total) |
| `SPEC-user-trigger.md` | **新增** 完整 PRD(323 行) |
| `CHANGELOG.md` | **新增** 本文件 |

### 已诊断问题(未修,等后续)

- 英文触发词 0/3 触发
- 极短 query(无上下文)触发率低
- 2 个 FP 来自 `Skill-Enrichment` 字面值(用户在改 SKILL.md / 问 skill 是什么,合理行为)

---

## v1.0 — 2026-05(初始版本,已弃用)

**核心机制**:被动事后触发——任务自动完成时,skill 主动判断是否反思。

### Description

```
Use when a procedural task has just finished — one that required applying a named skill, method, or multi-step procedure whose outcome depends on intermediate steps and is evaluable — and the agent needs to decide whether the procedure it used is fine, inefficient, defective, or merely not followed. Produces a typed reflection record (Discovery, Optimization, SkillDefect, ExecutionLapse) that drives targeted, non-destructive skill revision. (丰容 / Skill Enrichment — formerly known as Skill-Aware Reflection.)
```

### 退役原因

| 指标 | 值 | 影响 |
|---|---|---|
| Trigger recall | **0%** | skill 几乎从不触发 |
| 5 轮 description 优化 | 全 0% recall | 优化器对 description 措辞不敏感 |
| 实际根因 | `run_eval.py` 2 个 detection bug(早返回 + 大小写不匹配) | v1 描述实际**可能**工作,但 eval 检测不到 |

### 保留价值

- EmbodiSkill 四类反思框架(Discovery/Optimization/SkillDefect/ExecutionLapse)
- `S = (S_body, S_app)` 结构
- `literal comparison` 失败路径分类
- Quick Reference 决策树(graphviz)
- Discipline / Red Flags / Anti-rationalization / Common Mistakes
- Self-test 心理检查

**以上核心方法论在 v2 中完整保留,只是触发与执行流程改了。**

### v1 关键 commit 历史(可查)

| 范围 | commit | 说明 |
|---|---|---|
| 早期 | (skill-aware-reflection 仓库) | 论文移植、6 examples、6 evals |
| 重命名 | (本仓库 init) | skill-aware-reflection → Skill-Enrichment |
| README 系列 | `53cf7b6` `217b9f9` `91d1823` | 文档迭代,中文版同步 |
| Typing SVG | `663c7b3` | README 头部动态 SVG |
| v2.0 | `2542963` | 用户主动触发 + 任务盘点 + 确认门 |

---

## 版本规范

| 字段 | 说明 |
|---|---|
| 版本号 | SemVer:major.minor(只在这两个维度变化) |
| major | 触发机制或核心流程改变(v1 → v2) |
| minor | 描述措辞微调、eval 集调整、bug fix(不破坏触发) |
| 关联 commit | 必须列出 hash 以便 `git checkout <hash>` 回滚 |
| Trigger eval 数据 | 必须记录(评估"该版本是否解决了上一版的问题") |

---

## 触发机制决策树(历史视角)

```
v1 (废弃)  ── 失败  ──>  v2 (current)
                           │
"自动判定触发"             "用户主动触发"
   │                          │
   ▼                          ▼
Claude 自由裁量            确定性 string match
   │                          │
   ▼                          ▼
0% recall                 39% recall(目标 70%+)
```

**经验**:对于"反思/审计"这类**Claude 自带能力**相关的 skill,**不能依赖 Claude 自己的判定**——必须用显式触发词把"是否使用 skill"从"自由裁量"提升为"确定性匹配"。
