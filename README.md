<div align="right">

<a href="./README.zh.md">中文</a> · <a href="https://arxiv.org/abs/2605.10332v1">arXiv</a> · <a href="./CITATION.cff">Cite</a>

</div>

<img src="https://capsule-render.vercel.app/api?type=rect&height=4&color=3F5D3A&text=&fontSize=0" width="100%" alt=""/>

<!-- ============================================================
     HERO · 园丁手记封面
     ============================================================ -->
<div align="center">

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/h1.svg" alt="丰容 Skill Enrichment" height="110"/>

<br/>

<a href="https://arxiv.org/abs/2605.10332v1"><img src="https://img.shields.io/badge/MIT-Open%20Source-3F5D3A?style=flat-square&logo=opensourceinitiative&logoColor=white" alt="MIT"/></a>
<a href="https://www.anthropic.com/claude-code"><img src="https://img.shields.io/badge/Claude_Code-Skill-A3541E?style=flat-square&logo=anthropic&logoColor=white" alt="Claude Code"/></a>
<a href="https://arxiv.org/abs/2605.10332v1"><img src="https://img.shields.io/badge/EmbodiSkill-arXiv-3F5D3A?style=flat-square&logo=arxiv&logoColor=white" alt="arXiv"/></a>
<a href="./CITATION.cff"><img src="https://img.shields.io/badge/Cite-CFF-A87C2C?style=flat-square" alt="Cite"/></a>

<br/>

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/typing-en.svg" alt="Typing SVG" width="900"/>

<br/>

<table>
<tr>
<td align="center" width="33%">

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/card-en-1.svg" alt="Subject" height="32"/><br/>
<i>Procedural Skill</i>

</td>
<td align="center" width="33%">

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/card-en-2.svg" alt="Nourishment" height="32"/><br/>
<i>Task Trajectory</i>

</td>
<td align="center" width="33%">

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/card-en-3.svg" alt="Outcome" height="32"/><br/>
<i>Maturation · 0 → 1</i>

</td>
</tr>
</table>

</div>

---

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/h2-en-specimen-card.svg" alt="Specimen Card" height="42"/>

<table>
<tr><th align="left" width="22%">Field</th><th align="left">Value</th></tr>
<tr><td><b>Common name</b></td><td><b>丰容 / Skill Enrichment</b></td></tr>
<tr><td><b>Former name</b></td><td><i>Skill-Aware Reflection</i> (skill-aware-reflection)</td></tr>
<tr><td><b>Family</b></td><td>EmbodiSkill — <i>Self-Evolving Embodied Agents</i></td></tr>
<tr><td><b>Type locality</b></td><td>Ju et al., 2026 · arXiv:2605.10332v1 · <a href="https://arxiv.org/abs/2605.10332v1">link</a></td></tr>
<tr><td><b>Habitat</b></td><td><code>~/.claude/skills/Skill-Enrichment/</code></td></tr>
<tr><td><b>Diet</b></td><td>Real task trajectories (the <b>core nourishment</b>)</td></tr>
<tr><td><b>Keeper</b></td><td>The agent itself, under the four-type reflection framework</td></tr>
<tr><td><b>Conservation status</b></td><td>

`MIT` — open source · `arXiv preprint` — academic citation required

</td></tr>
</table>

---

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/h2-en-on-the-name.svg" alt="On the Name" height="42"/>

> *In the animal-welfare sciences, **environmental enrichment** is the practice of providing captive animals with diverse, biologically meaningful stimuli — to satisfy their physiological and psychological needs, promote natural behavior, and reduce stereotypy.*
>
> *This project borrows that idea — literally.*

| Domain | Captive setting (animal welfare) | Claude Code (this project) |
|---|---|---|
| Subject of enrichment | Captive animal | Procedural skill |
| Enriching stimulus | Diverse environment | Real task trajectories |
| Target behavior | Natural behavior display | Cross-scenario procedural competence |
| Behavior to avoid | Stereotypy (repetitive, purposeless) | Force-fitting the same outdated fix to every new case |
| Enricher | Zookeeper | Agent (under the reflection framework) |

The metaphor is not decoration — it is the project's organizing principle:

> <b>No trajectory, no enrichment.</b> A skill that never sees a real run is a skill that never matures.

### What is in a name?

| Term | Role |
|---|---|
| **EmbodiSkill** | Framework name (paper) |
| **Skill-Aware Reflection** | Sub-method name inside the paper's framework |
| **丰容 / Skill Enrichment** | This engineering project — names the *stimulus → maturation* process as a whole |

---

<table>
<tr><td>

> ### ⟁ Academic Attribution
>
> <b>This skill is an engineering port of the paper EmbodiSkill, not an independent original method.</b>
>
> The core methodology — the four-type reflection framework, the `S = (S_body, S_app)` revision structure, the classification logic — is by Ju et al. (2026, arXiv:2605.10332).
>
> This repository's engineering contributions are detailed in [`SKILL.md - Academic Attribution`](./SKILL.md#-academic-attribution).
>
> <b>By using this skill you agree</b>: any academic or commercial use that cites this skill must also cite the original paper.

</td></tr>
</table>

---

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/h2-en-how-it-works.svg" alt="How It Works" height="42"/>

After a **procedural task** finishes — one that applied a named skill, method, or multi-step procedure whose outcome depends on intermediate steps — this skill forces the agent to classify what happened into one of **four types** and produce a targeted, non-destructive revision of the underlying skill.

> *The defining test*: did the agent follow a procedure with ≥2 ordered steps where the result depended on intermediate state? If no — this skill does not apply.

### The Four Reflection Types

<table>
<tr><th width="14%">Animal</th><th width="18%">Type</th><th width="24%">Trigger</th><th width="24%">Action</th><th width="20%">Modifies</th></tr>
<tr><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/animal-fox.svg" alt="fox" width="100"/></td><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/chip-discovery.svg" alt="Discovery 发现" height="64"/></td><td>Success + new capability the skill doesn't cover</td><td>Record new skill seed</td><td><code>S_body</code> (append)</td></tr>
<tr><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/animal-bird.svg" alt="bird" width="100"/></td><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/chip-optimization.svg" alt="Optimization 优化" height="64"/></td><td>Success + an existing paragraph has a better form</td><td>Replace or complete the targeted paragraph</td><td><code>S_body</code> (replace / complete)</td></tr>
<tr><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/animal-tree.svg" alt="tree" width="100"/></td><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/chip-skilldefect.svg" alt="SkillDefect 技能缺陷" height="64"/></td><td>Failure + the paragraph is wrong, incomplete, or underspecified</td><td>Replace or complete the targeted paragraph</td><td><code>S_body</code> (replace / complete)</td></tr>
<tr><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/animal-octopus.svg" alt="octopus" width="100"/></td><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/chip-executionlapse.svg" alt="ExecutionLapse 执行偏差" height="64"/></td><td>Failure + paragraph is valid but the agent did not follow it</td><td>Append a reminder to the execution appendix</td><td><code>S_app</code> <b>only</b> — never <code>S_body</code></td></tr>
</table>

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/h2-en-one-question-test.svg" alt="The One-Question Test" height="42"/>

> *"If the agent had followed the paragraph to the letter, would the task have succeeded?"*
>
> * Yes → **ExecutionLapse**
> * No → **SkillDefect**
>
> The most error-prone boundary is `SkillDefect ↔ ExecutionLapse`. The skill provides a [literal-comparison method](./examples.md#example-6) to disambiguate them.

---

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/h2-en-differentiation-hermes.svg" alt="Differentiation" height="42"/>

> *Common question: how does this differ from hermes-agent?*
> *Short answer: **they are not competitors** — they target different users and different needs.*

### 5.1 Jobs to be Done

| 丰容 / Skill Enrichment | hermes-agent |
|---|---|
| When one of my Claude Code skills underperforms in some scenarios, I want to **precisely identify and surgically fix** the specific bad paragraph — not rewrite the whole skill — so I keep what's already correct and avoid the side effects of wholesale rewrites. | When I want a **24×7, cross-platform, remembering, learning-from-experience** personal AI assistant, I don't want to assemble memory systems, schedulers, message gateways, and skill frameworks myself — I want an out-of-the-box system that grows with me over the long term. |

### 5.2 Need hierarchy

| Need layer | 丰容 | hermes-agent |
|---|---|---|
| Functional | Paragraph-level targeted revision + 4-type classification | Multi-platform + multi-backend + automatic skill creation |
| Reliability | Prevents "bad edits" (guards against 3 documented systematic problems) | Prevents "data loss" (auto-archive + FTS5 search) |
| Usability | Available as soon as Claude Code's description trigger fires | Available from terminal + Telegram + Discord + … |
| Growth | A single skill paragraph gets more accurate over time | The whole agent becomes more attuned to the user |
| Pain eliminated | "My skill won't change / gets worse when I edit it" | "My agent doesn't remember / I can't find past work" |
| Investment style | One-shot precision work | Cumulative long-term investment |

### 5.3 Need-solution matrix

| User need | 丰容 | hermes-agent | Solved better by |
|---|---|---|---|
| "Which paragraph of my skill is broken?" | ✅ explicit + paragraph-level | ⚠️ LLM judgment | 丰容 |
| "I want an AI I can talk to from anywhere" | ❌ Claude Code only | ✅ CLI + Telegram + Discord + … | hermes-agent |
| "I want my agent to remember me across sessions" | ❌ no auto-mechanism | ✅ FTS5 + LLM summaries | hermes-agent |
| "I want a skill to appear without me writing it" | ❌ does not create | ✅ Curator distills | hermes-agent |
| "I want strict guarantees that skills won't be corrupted" | ✅ 4-type forced + `S_app` isolation | ⚠️ no explicit classification | 丰容 |
| "I want stale skills auto-archived" | ❌ manual | ✅ `stale_after_days` | hermes-agent |
| "I'm already in Claude Code and won't install new things" | ✅ one-skill install | ❌ full agent system install | 丰容 |
| "I want my agent to grow more attuned to me over time" | ❌ single-turn precision | ✅ closed-loop learning + persistence | hermes-agent |

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

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/h2-en-installation.svg" alt="Installation" height="42"/>

```bash
# Option 1 — Unzip the packaged .skill file
unzip Skill-Enrichment.skill -d ~/.claude/skills/

# Option 2 — Clone the repo (after rename)
git clone https://github.com/z77orz/Skill-Enrichment.git \
    ~/.claude/skills/Skill-Enrichment
```

The skill is auto-discovered by Claude Code once placed under `~/.claude/skills/Skill-Enrichment/`.

---

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/h2-en-repository-layout.svg" alt="Repository Layout" height="42"/>

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
├── assets/                   # Field Guide SVG assets (this README references them)
├── README.md                 # This file (English)
├── README.zh.md              # 中文版
├── CITATION.cff
└── LICENSE
```

---

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/h2-en-validation.svg" alt="Validation" height="42"/>

The skill was validated against 4 benchmark evals.

| Configuration | Pass rate | Time | Tokens |
|---|---|---|---|
| **With Skill** | **100 %** | 62.3 s ± 12.3 s | 73,525 |
| Without Skill | 64 % | 50.9 s ± 5.8 s | 69,211 |
| **Delta** | **+0.36** | +11.5 s | +4,314 |

**Largest discriminator**: `SkillDefect` classification — baseline scored **25 %** (1/4) where with-skill scored **100 %** (4/4). Without the framework, agents tend to misclassify skill-content defects as execution lapses or produce vague patches.

To reproduce, run the 4 standard-format prompts in [`evals/evals.json`](./evals/evals.json) with and without the skill installed.

---

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/h2-en-citation.svg" alt="Citation" height="42"/>

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

(The arXiv ID is the permanent identifier; no journal DOI exists yet.)

---

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/h2-en-license.svg" alt="License" height="42"/>

`MIT` — see [`LICENSE`](./LICENSE). The MIT notice covers this engineering port; the underlying methodology remains that of the EmbodiSkill authors.

<br/>

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=rect&height=2&color=3F5D3A&text=&fontSize=0" width="100%" alt=""/>

<br/>

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/h2-en-repository-activity.svg" alt="Repository activity" height="42"/>

<br/>

<img src="https://github-readme-activity-graph.vercel.app/graph?username=z77orz&theme=github-compact&hide_border=true&area=true&bg_color=FAF7F0&color=3F5D3A&line=A3541E&point=A87C2C&hide_title=false" alt="Activity graph" width="92%"/>

</div>

---

<div align="center">

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/footer-star-moss.svg" alt="✦" height="40"/> This README follows the <i>Field Guide</i> aesthetic — a tribute to the 19th-century practice of natural-history field guides. <img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/footer-star-moss.svg" alt="✦" height="40"/>

<br/>

<sub>Designed for GitHub Markdown rendering. Best viewed in light mode.</sub>

</div>
