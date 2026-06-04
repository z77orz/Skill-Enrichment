<div align="right">

<a href="./README.zh.md">中文</a> · <a href="https://arxiv.org/abs/2605.10332v1">arXiv</a> · <a href="./CITATION.cff">Cite</a>

</div>

<img src="https://capsule-render.vercel.app/api?type=rect&height=4&color=3F5D3A&text=&fontSize=0" width="100%" alt=""/>

<!-- ============================================================
     HERO · Field Guide Cover
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
<tr><td><b>Former name</b></td><td><i>Skill-Aware Reflection</i> (skill-aware-reflection repo)</td></tr>
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
> Engineering contributions of this repository are detailed in [`SKILL.md`](./SKILL.md).
>
> <b>By using this skill you agree</b>: any academic or commercial use that cites this skill must also cite the original paper.

</td></tr>
</table>

---

## Quick Start

### Installation

```bash
# Option 1 — Unzip the packaged .skill file
unzip Skill-Enrichment.skill -d ~/.claude/skills/

# Option 2 — Clone the repo
git clone https://github.com/z77orz/Skill-Enrichment.git \
    ~/.claude/skills/Skill-Enrichment
```

The skill is auto-discovered by Claude Code once placed under `~/.claude/skills/Skill-Enrichment/`.

### Usage

Say any of these trigger phrases in Claude Code to activate:

| Type | Examples |
|---|---|
| Primary (Chinese) | 反思技能 / 进化技能 / 优化技能 |
| Derivative (Chinese) | 复盘技能 / 丰容技能 / 技能复盘 |
| English equivalents | reflect on skill / evolve skill / optimize skill |

**Typical session**:

```
You: reflect on skill — I ran contract-review a few times today,
      some went well, some failed. Let me review them.

→ Skill-Enrichment scans the current session and lists executed tasks
→ You pick (task, skill) combinations to reflect on
→ A reflection record draft is generated for your review
→ You confirm before any SKILL.md is edited
```

**Full pipeline** (6 steps):

```text
Step 0: Trigger Verification  ←─ description semantic recall + Step 0 mechanical match
   │
   ▼
Step 1: Task Inventory        ←─ Scan session for (task, skill) pairs
   │
   ▼
Step 2: User Selection        ←─ You pick combinations to reflect on
   │
   ├─ Same skill ≥ 2 times? → Step 2.5: Per-task vs aggregate
   │
   ▼
Step 3: Generate Record       ←─ Four-type classification (Discovery/Optimization/SkillDefect/ExecutionLapse)
   │
   ▼
Step 4: Confirmation Gate     ←─ Record is shown for review; no file is modified yet
   │   ├─ Accept → Step 5
   │   ├─ Reject → Log as rejected
   │   └─ Modify → Regenerate
   │
   ▼
Step 5: Safety Check + Edit   ←─ b_i uniqueness / line-change ≤ 50% / directive enum validation
   │
   ▼
Audit Log                     ←─ Recorded to reflections/YYYY-MM-DD.md
```

---

## How It Works

After a **procedural task** finishes — one that applied a named skill, method, or multi-step procedure whose outcome depends on intermediate steps — this skill forces the agent to classify what happened into one of **four types** and produce a targeted, non-destructive revision of the underlying skill. Never a whole-skill rewrite.

### The Four Reflection Types

<table>
<tr><th width="14%">Animal</th><th width="18%">Type</th><th width="24%">Trigger</th><th width="24%">Action</th><th width="20%">Modifies</th></tr>
<tr><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/animal-fox.svg" alt="fox" width="100"/></td><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/chip-discovery.svg" alt="Discovery" height="64"/></td><td>Success + new capability the skill doesn't cover</td><td>Record new skill seed</td><td><code>S_body</code> (append)</td></tr>
<tr><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/animal-bird.svg" alt="bird" width="100"/></td><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/chip-optimization.svg" alt="Optimization" height="64"/></td><td>Success + an existing paragraph has a better form</td><td>Replace or complete the targeted paragraph</td><td><code>S_body</code> (replace/complete)</td></tr>
<tr><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/animal-tree.svg" alt="tree" width="100"/></td><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/chip-skilldefect.svg" alt="SkillDefect" height="64"/></td><td>Failure + the paragraph is wrong, incomplete, or underspecified</td><td>Replace or complete the targeted paragraph</td><td><code>S_body</code> (replace/complete)</td></tr>
<tr><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/animal-octopus.svg" alt="octopus" width="100"/></td><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/chip-executionlapse.svg" alt="ExecutionLapse" height="64"/></td><td>Failure + paragraph is valid but the agent did not follow it</td><td>Append a reminder to the execution appendix</td><td><code>S_app</code> <b>only</b> — never <code>S_body</code></td></tr>
</table>

### The One-Question Test

> *"If the agent had followed the paragraph to the letter, would the task have succeeded?"*
>
> * Yes → **ExecutionLapse**
> * No → **SkillDefect**
>
> The most error-prone boundary is `SkillDefect ↔ ExecutionLapse`. The skill provides a [literal-comparison method](./examples.md#example-6) to disambiguate them.

---

## Repository Layout

```text
Skill-Enrichment/
├── SKILL.md                  # Main body (267 lines, optimized — read this first)
├── examples.md               # 6 worked examples, one per reflection type
├── reflection-record.md      # Template for emitting reflection records
├── evals/
│   └── evals.json            # 20 trigger eval prompts
├── tests/                    # TDD artifacts (RED / REFACTOR phases)
│   ├── pressure-scenarios.md
│   ├── baseline-failures.md
│   └── verification.md
├── assets/                   # Field Guide SVG assets
├── README.md                 # This file (English)
├── README.zh.md              # 中文版
├── CHANGELOG.md              # description change history
├── SPEC-user-trigger.md      # v2 PRD document
├── CITATION.cff
└── LICENSE
```

---

## Validation

Validated against 20 trigger eval prompts (see [`evals/evals.json`](./evals/evals.json)).

| Configuration | Pass rate | Time | Tokens |
|---|---|---|---|
| **With Skill** | **100 %** | 62.3 s ± 12.3 s | 73,525 |
| Without Skill | 64 % | 50.9 s ± 5.8 s | 69,211 |
| **Delta** | **+0.36** | +11.5 s | +4,314 |

**Largest discriminator**: `SkillDefect` classification — baseline scored **25 %** (1/4) where with-skill scored **100 %** (4/4). Without the framework, agents tend to misclassify skill-content defects as execution lapses or produce vague patches.

### v2 Optimization Results

| Metric | v1 (passive trigger) | v2 (user-initiated) | v2 Optimized (current) |
|---|---|---|---|
| Trigger recall | 0% | 39% | Under optimization (≤250 char description in test) |
| SKILL.md size | 464 lines | 499 lines | **267 lines** (−46.5%) |
| Trigger mode | Automatic detection | Explicit trigger phrase | Same as v2, more precise |

---

## Citation

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

## License

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
