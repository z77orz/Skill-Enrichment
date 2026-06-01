# Skill-Aware Reflection

> 中文版：[README.zh.md](./README.zh.md)

A Claude Code / Claude.ai skill that operationalizes the four-type skill-aware reflection framework from [EmbodiSkill (Ju et al., 2026)](https://arxiv.org/abs/2605.10332v1).

After a non-trivial task finishes, this skill forces the agent to classify what happened into one of four types and produce a targeted, non-destructive revision of the underlying skill — never a coarse whole-skill rewrite.

## The Four Reflection Types

| Type | Trigger | Action | Modifies |
|---|---|---|---|
| **Discovery** | Success + new capability the skill doesn't cover | Record new skill seed | `S_body` (append) |
| **Optimization** | Success + an existing paragraph has a better form | Replace or complete the targeted paragraph | `S_body` (replace / complete) |
| **SkillDefect** | Failure + the paragraph is wrong, incomplete, or underspecified | Replace or complete the targeted paragraph | `S_body` (replace / complete) |
| **ExecutionLapse** | Failure + paragraph is valid but the agent did not follow it | Append a reminder to the execution appendix | `S_app` only — never `S_body` |

The most error-prone boundary is **SkillDefect vs ExecutionLapse**. The skill provides a literal-comparison method to disambiguate them, and a one-question test: *"If the agent had followed the paragraph to the letter, would the task have succeeded?"* — Yes → ExecutionLapse, No → SkillDefect.

## Why

Existing skill self-evolution methods are *skill-unaware*: they convert trajectories into general feedback and rewrite the whole skill. EmbodiSkill shows this accumulates redundant content, overwrites valid guidance, and preserves incorrect prescriptions. The four-type classification fixes that.

## When to Use

Use when **all** of the following hold:

- A non-trivial task has just finished (not a one-step lookup).
- The task used at least one skill, sub-skill, or named procedure.
- The task outcome is evaluable: success, partial success, or failure.

Do NOT use for one-off tool calls with no procedural skill involved.

## Installation

```bash
# Option 1: Unzip the packaged .skill file
unzip skill-aware-reflection.skill -d ~/.claude/skills/

# Option 2: Clone the repo
git clone https://github.com/z77orz/skill-aware-reflection.git \
    ~/.claude/skills/skill-aware-reflection
```

The skill is auto-discovered by Claude Code and Claude.ai once placed under `~/.claude/skills/`.

## Repository Structure

```
skill-aware-reflection/
├── SKILL.md                  # Main reference (read this first)
├── examples.md               # 6 worked examples, one per reflection type
├── reflection-record.md      # Template for emitting reflection records
├── evals/
│   └── evals.json            # 4 standard-format test prompts
├── tests/                    # TDD artifacts (RED / REFACTOR phases)
│   ├── pressure-scenarios.md # 6 pressure scenarios
│   ├── baseline-failures.md  # 8 baseline failure modes the skill blocks
│   └── verification.md       # Cross-check that skill addresses each scenario
└── README.md
```

## Validation

The skill was validated against 4 benchmark evals. Results:

| Configuration | Pass Rate | Time | Tokens |
|---|---|---|---|
| **With Skill** | **100%** | 62.3s ± 12.3s | 73,525 |
| Without Skill | 64% | 50.9s ± 5.8s | 69,211 |
| **Delta** | **+0.36** | +11.5s | +4,314 |

Largest discriminator: `SkillDefect` classification — baseline scored 25% (1/4) where with-skill scored 100% (4/4). Without the framework, agents tend to misclassify skill-content defects as execution lapses or produce vague patches.

To reproduce: see `~/.claude/skills/skill-aware-reflection-workspace/` (in the local development environment) for the `grade.py` and `aggregate_benchmark.py` scripts.

## Citation

```bibtex
@article{ju2026embodiskill,
  title={EmbodiSkill: Skill-Aware Reflection for Self-Evolving Embodied Agents},
  author={Ju, Ruofei and Wang, Xinrui and Ding, Xin and Yang, Yifan and Wu, Hao and Jiang, Shiqi and Zhang, Qianxi and Wen, Hao and Li, Xiangyu and Wang, Meijun and Li, Kun and Liu, Yunxin and Dai, Haipeng and Wang, Wei and Cao, Ting},
  journal={arXiv preprint arXiv:2605.10332},
  year={2026}
}
```

## License

MIT
