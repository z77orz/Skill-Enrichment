<div align="right">

<a href="./README.zh.md">中文</a> · <a href="https://arxiv.org/abs/2605.10332v1">arXiv</a> · <a href="./CITATION.cff">Cite</a>

</div>

<!-- ============================================================
     HERO · 园丁手记封面
     ============================================================ -->
<div align="center">

<!-- 字体预连接: GitHub 在沙箱里无法下载 woff 文件,
     但 <link> 标签可以引导用户浏览器解析 head 注入,
     这里改成在 README 顶部用注释给出,避免渲染警告 -->

# ✦ 丰容 (Skill Enrichment) ✦

### *A Field Guide to Procedural-Skill Maturation in Claude Code*

*formerly **Skill-Aware Reflection** — an EmbodiSkill port (Ju et al., 2026, arXiv:2605.10332)*

<br/>

<table>
<tr>
<td align="center" width="33%">

**⟁ Subject**  
*Procedural Skill*

</td>
<td align="center" width="33%">

**⟐ Nourishment**  
*Task Trajectory*

</td>
<td align="center" width="33%">

**⟁ Outcome**  
*Maturation · 0 → 1*

</td>
</tr>
</table>

<br/>

```text
> In captive settings, the keeper's craft is enrichment.
> In Claude Code, this keeper is the agent, this captive is the skill,
> and the trajectory is the meal.
```

</div>

---

<!-- ============================================================
     SECTION 1 · 学名卡 / 物种介绍
     ============================================================ -->
## ⟐ Specimen Card

<table>
<tr>
<th align="left" width="22%">Field</th>
<th align="left">Value</th>
</tr>
<tr>
<td><b>Common name</b></td>
<td><b>丰容 / Skill Enrichment</b></td>
</tr>
<tr>
<td><b>Former name</b></td>
<td><i>Skill-Aware Reflection</i> (skill-aware-reflection)</td>
</tr>
<tr>
<td><b>Family</b></td>
<td>EmbodiSkill — <i>Self-Evolving Embodied Agents</i></td>
</tr>
<tr>
<td><b>Type locality</b></td>
<td>Ju et al., 2026 · arXiv:2605.10332v1 · <a href="https://arxiv.org/abs/2605.10332v1">link</a></td>
</tr>
<tr>
<td><b>Habitat</b></td>
<td><code>~/.claude/skills/Skill-Enrichment/</code></td>
</tr>
<tr>
<td><b>Diet</b></td>
<td>Real task trajectories (the <b>core nourishment</b>)</td>
</tr>
<tr>
<td><b>Keeper</b></td>
<td>The agent itself, under the four-type reflection framework</td>
</tr>
<tr>
<td><b>Conservation status</b></td>
<td>

`MIT` — open source · `arXiv preprint` — academic citation required

</td>
</tr>
</table>

---

<!-- ============================================================
     SECTION 2 · 命名志 / Etymology
     ============================================================ -->
## ✦ On the Name

> *In the animal-welfare sciences, **environmental enrichment** is the practice of providing captive animals with diverse, biologically meaningful stimuli — to satisfy their physiological and psychological needs, promote natural behavior, and reduce stereotypy.*
>
> *This project borrows that idea — literally.*

| Domain | Captive setting (animal welfare) | Claude Code (this project) |
|---|---|---|
| Subject of enrichment | Captive animal | Procedural skill |
| Enriching stimulus | Diverse environment | Real task trajectories |
| Target behavior | Natural behavior display | Cross-scenario procedural competence |
| Behavior to avoid | Stereotypy (repetitive, purposeless) | Reapplying an outdated `b_i` to every new case |
| Enricher | Zookeeper | Agent (under the reflection framework) |

The metaphor is not decoration — it is the project's organizing principle:

> **No trajectory, no enrichment.** A skill that never sees a real run is a skill that never matures.

### What is in a name?

| Term | Role |
|---|---|
| **EmbodiSkill** | Framework name (paper) |
| **Skill-Aware Reflection** | Sub-method name inside the paper's framework |
| **丰容 / Skill Enrichment** | This engineering project — names the *stimulus → maturation* process as a whole |

---

<!-- ============================================================
     SECTION 3 · 学术归属 / Provenance (框中框)
     ============================================================ -->
<table>
<tr>
<td>

> ### ⟁ Academic Attribution
>
> **This skill is an engineering port of the paper EmbodiSkill, not an independent original method.**
>
> The core methodology — the four-type reflection framework, the `S = (S_body, S_app)` revision structure, the classification logic — is by Ju et al. (2026, arXiv:2605.10332).
>
> This repository's engineering contributions are detailed in [`SKILL.md - Academic Attribution`](./SKILL.md#-academic-attribution).
>
> **By using this skill you agree**: any academic or commercial use that cites this skill must also cite the original paper.

</td>
</tr>
</table>

---

<!-- ============================================================
     SECTION 4 · 工作机制 / Mechanism
     ============================================================ -->
## ⟐ How It Works

After a **procedural task** finishes — one that applied a named skill, method, or multi-step procedure whose outcome depends on intermediate steps — this skill forces the agent to classify what happened into one of **four types** and produce a targeted, non-destructive revision of the underlying skill.

> *The defining test*: did the agent follow a procedure with ≥2 ordered steps where the result depended on intermediate state? If no — this skill does not apply.

### The Four Reflection Types

<table>
<tr>
<th width="14%">Type</th>
<th width="32%">Trigger</th>
<th width="32%">Action</th>
<th width="22%">Modifies</th>
</tr>
<tr>
<td><span style="color:#3F5D3A"><b>🔍 Discovery</b></span></td>
<td>Success + new capability the skill doesn't cover</td>
<td>Record new skill seed</td>
<td><code>S_body</code> (append)</td>
</tr>
<tr>
<td><span style="color:#A3541E"><b>⚙️ Optimization</b></span></td>
<td>Success + an existing paragraph has a better form</td>
<td>Replace or complete the targeted paragraph</td>
<td><code>S_body</code> (replace / complete)</td>
</tr>
<tr>
<td><span style="color:#8B2C1F"><b>⚠️ SkillDefect</b></span></td>
<td>Failure + the paragraph is wrong, incomplete, or underspecified</td>
<td>Replace or complete the targeted paragraph</td>
<td><code>S_body</code> (replace / complete)</td>
</tr>
<tr>
<td><span style="color:#4A4A4A"><b>⏸ ExecutionLapse</b></span></td>
<td>Failure + paragraph is valid but the agent did not follow it</td>
<td>Append a reminder to the execution appendix</td>
<td><code>S_app</code> <b>only</b> — never <code>S_body</code></td>
</tr>
</table>

> ### ⟐ The One-Question Test
>
> *"If the agent had followed the paragraph to the letter, would the task have succeeded?"*
>
> * Yes → **ExecutionLapse**
> * No → **SkillDefect**
>
> The most error-prone boundary is `SkillDefect ↔ ExecutionLapse`. The skill provides a [literal-comparison method](./examples.md#example-6) to disambiguate them.

---

<!-- ============================================================
     SECTION 5 · 与 hermes-agent 的差异 / Differentiation
     ============================================================ -->
## ✦ Differentiation from hermes-agent

> *Common question: how does this differ from hermes-agent?*
> *Short answer: **they are not competitors** — they target different users and different needs.*

### 5.1 Jobs to be Done

<table>
<tr>
<th width="50%">丰容 / Skill Enrichment</th>
<th width="50%">hermes-agent</th>
</tr>
<tr>
<td valign="top">

When one of my Claude Code skills underperforms in some scenarios, I want to **precisely identify and surgically fix** the specific bad paragraph — not rewrite the whole skill — so I keep what's already correct and avoid the side effects of wholesale rewrites.

</td>
<td valign="top">

When I want a **24×7, cross-platform, remembering, learning-from-experience** personal AI assistant, I don't want to assemble memory systems, schedulers, message gateways, and skill frameworks myself — I want an out-of-the-box system that grows with me over the long term.

</td>
</tr>
</table>

### 5.2 Need hierarchy

<table>
<tr>
<th width="20%">Need layer</th>
<th width="40%">丰容</th>
<th width="40%">hermes-agent</th>
</tr>
<tr>
<td><b>Functional</b></td>
<td>Paragraph-level targeted revision + 4-type classification</td>
<td>Multi-platform + multi-backend + automatic skill creation</td>
</tr>
<tr>
<td><b>Reliability</b></td>
<td>Prevents "bad edits" (guards against 3 documented systematic problems)</td>
<td>Prevents "data loss" (auto-archive + FTS5 search)</td>
</tr>
<tr>
<td><b>Usability</b></td>
<td>Available as soon as Claude Code's description trigger fires</td>
<td>Available from terminal + Telegram + Discord + …</td>
</tr>
<tr>
<td><b>Growth</b></td>
<td>A single skill paragraph gets more accurate over time</td>
<td>The whole agent becomes more attuned to the user</td>
</tr>
<tr>
<td><b>Pain eliminated</b></td>
<td>"My skill won't change / gets worse when I edit it"</td>
<td>"My agent doesn't remember / I can't find past work"</td>
</tr>
<tr>
<td><b>Investment style</b></td>
<td>One-shot precision work</td>
<td>Cumulative long-term investment</td>
</tr>
</table>

### 5.3 Need-solution matrix

<table>
<tr>
<th>User need</th>
<th width="22%">丰容</th>
<th width="22%">hermes-agent</th>
<th width="30%">Solved better by</th>
</tr>
<tr>
<td>"Which paragraph of my skill is broken?"</td>
<td align="center">✅ explicit + paragraph-level</td>
<td align="center">⚠️ LLM judgment</td>
<td align="center"><b>丰容</b></td>
</tr>
<tr>
<td>"I want an AI I can talk to from anywhere"</td>
<td align="center">❌ Claude Code only</td>
<td align="center">✅ CLI + Telegram + Discord + …</td>
<td align="center"><b>hermes-agent</b></td>
</tr>
<tr>
<td>"I want my agent to remember me across sessions"</td>
<td align="center">❌ no auto-mechanism</td>
<td align="center">✅ FTS5 + LLM summaries</td>
<td align="center"><b>hermes-agent</b></td>
</tr>
<tr>
<td>"I want a skill to appear without me writing it"</td>
<td align="center">❌ does not create</td>
<td align="center">✅ Curator distills</td>
<td align="center"><b>hermes-agent</b></td>
</tr>
<tr>
<td>"I want strict guarantees that skills won't be corrupted"</td>
<td align="center">✅ 4-type forced + <code>S_app</code> isolation</td>
<td align="center">⚠️ no explicit classification</td>
<td align="center"><b>丰容</b></td>
</tr>
<tr>
<td>"I want stale skills auto-archived"</td>
<td align="center">❌ manual</td>
<td align="center">✅ <code>stale_after_days</code></td>
<td align="center"><b>hermes-agent</b></td>
</tr>
<tr>
<td>"I'm already in Claude Code and won't install new things"</td>
<td align="center">✅ one-skill install</td>
<td align="center">❌ full agent system install</td>
<td align="center"><b>丰容</b></td>
</tr>
<tr>
<td>"I want my agent to grow more attuned to me over time"</td>
<td align="center">❌ single-turn precision</td>
<td align="center">✅ closed-loop learning + persistence</td>
<td align="center"><b>hermes-agent</b></td>
</tr>
</table>

### 5.4 Decision tree

```text
Are you mainly a Claude Code user?
├── Yes → Is your pain point skill maintenance?
│       ├── Yes → 丰容 ✅
│       └── No (you want multi-platform / long-term memory)
│           → you actually need hermes-agent
│
└── No → Do you want your own AI agent?
        ├── Yes (willing to install a full system) → hermes-agent ✅
        └── No (you just want occasional use) → neither
```

> **One-liner**: 丰容 is a **surgeon** — it precisely fixes what already exists. hermes-agent is a **long-term assistant** — it grows with you from experience. The two are **complementary, not competing**.

---

<!-- ============================================================
     SECTION 6 · 安装 / Installation
     ============================================================ -->
## ⟐ Installation

```bash
# Option 1 — Unzip the packaged .skill file
unzip Skill-Enrichment.skill -d ~/.claude/skills/

# Option 2 — Clone the repo (after rename)
git clone https://github.com/z77orz/Skill-Enrichment.git \
    ~/.claude/skills/Skill-Enrichment
```

<<<<<<< HEAD
The skill is auto-discovered by Claude Code once placed under `~/.claude/skills/`.
=======
The skill is auto-discovered by Claude Code once placed under `~/.claude/skills/Skill-Enrichment/`.
>>>>>>> acd66be (refactor: rebrand to 丰容 / Skill Enrichment)

---

<!-- ============================================================
     SECTION 7 · 仓库结构 / Repository layout
     ============================================================ -->
## ⟐ Repository Layout

```text
Skill-Enrichment/
├── SKILL.md                  # Main reference (read this first)
├── examples.md               # 6 worked examples, one per reflection type
├── reflection-record.md      # Template for emitting reflection records
├── evals/
│   └── evals.json            # 4 standard-format test prompts
├── tests/                    # TDD artifacts (RED / REFACTOR phases)
│   ├── pressure-scenarios.md
│   ├── baseline-failures.md
│   └── verification.md
├── README.md                 # This file (English)
├── README.zh.md              # 中文版
├── CITATION.cff
└── LICENSE
```

---

<!-- ============================================================
     SECTION 8 · 验证 / Validation
     ============================================================ -->
## ✦ Validation

The skill was validated against 4 benchmark evals.

<table>
<tr>
<th align="left">Configuration</th>
<th align="right">Pass rate</th>
<th align="right">Time</th>
<th align="right">Tokens</th>
</tr>
<tr>
<td><b>With Skill</b></td>
<td align="right"><b>100 %</b></td>
<td align="right">62.3 s ± 12.3 s</td>
<td align="right">73,525</td>
</tr>
<tr>
<td>Without Skill</td>
<td align="right">64 %</td>
<td align="right">50.9 s ± 5.8 s</td>
<td align="right">69,211</td>
</tr>
<tr>
<td><b>Delta</b></td>
<td align="right"><b>+0.36</b></td>
<td align="right">+11.5 s</td>
<td align="right">+4,314</td>
</tr>
</table>

**Largest discriminator**: `SkillDefect` classification — baseline scored **25 %** (1/4) where with-skill scored **100 %** (4/4). Without the framework, agents tend to misclassify skill-content defects as execution lapses or produce vague patches.

To reproduce: see `~/.claude/skills/skill-aware-reflection-workspace/` (a sibling dev workspace that preserves the original project name for benchmark-result continuity) for the `grade.py` and `aggregate_benchmark.py` scripts.

---

<!-- ============================================================
     SECTION 9 · 引用 / Citation
     ============================================================ -->
## ⟐ Citation

If you use this skill in research or write a paper that benefits from the underlying framework, please cite the original EmbodiSkill paper (arXiv preprint, not yet peer-reviewed):

```bibtex
@misc{ju2026embodiskill,
  title        = {EmbodiSkill: Skill-Aware Reflection for Self-Evolving Embodied Agents},
  author       = {Ju, Ruofei and Wang, Xinrui and Ding, Xin and Yang, Yifan and Wu, Hao and Jiang, Shiqi and Zhang, Qianxi and Wen, Hao and Li, Xiangyu and Wang, Meijun and Li, Kun and Liu, Yunxin and Dai, Haipeng and Wang, Wei and Cao, Ting},
  year         = {2026},
  eprint       = {2605.10332},
  archivePrefix= {arXiv},
  primaryClass = {cs.AI},
  note         = {Corresponding author: Cao, Ting (tingcao@mail.tsinghua.edu.cn)}
}
```

**In-text citation form** (used throughout this repository):
* Parenthetical: `(Ju et al., 2026, arXiv:2605.10332)`
* Narrative: `Ju et al. (2026, arXiv:2605.10332)`

The arXiv ID is included in the in-text form because this is a preprint without a journal DOI; the ID is the only permanent identifier.

---

<!-- ============================================================
     SECTION 10 · 许可 / License
     ============================================================ -->
## ⟐ License

`MIT` — see [`LICENSE`](./LICENSE). The MIT notice covers this engineering port; the underlying methodology remains that of the EmbodiSkill authors.

<br/>

---

<div align="center">

<sub>✦ This README follows the *Field Guide* aesthetic — a tribute to the 19th-century practice of natural-history field guides. ✦</sub>

<br/>

<sub>Designed for GitHub Markdown rendering. Best viewed in light mode.</sub>

</div>
