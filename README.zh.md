# 技能感知反思（Skill-Aware Reflection）

> English version: [README.md](./README.md)

一个 Claude Code 技能，将论文 [EmbodiSkill (Ju et al., 2026)](https://arxiv.org/abs/2605.10332v1) 的"四类技能感知反思"框架工程化。

每完成一个**程序性任务**后（指应用了某个具名 skill、流程或多步程序、其结果依赖中间步骤的任务），本技能强制 agent 把"刚才发生了什么"归入四种类型之一，并对底层 skill 做出**有针对性的、非破坏性的**修订 —— 绝不整体重写。

## 四类反思

| 类型 | 触发条件 | 动作 | 修改对象 |
|---|---|---|---|
| **Discovery（发现）** | 成功 + 出现 skill 未覆盖的新能力 | 记录新 skill 种子 | `S_body`（追加）|
| **Optimization（优化）** | 成功 + 现有段落有更优形式 | 替换或补全目标段落 | `S_body`（替换/补全）|
| **SkillDefect（技能缺陷）** | 失败 + 段落本身错误、不完整或未明确 | 替换或补全目标段落 | `S_body`（替换/补全）|
| **ExecutionLapse（执行偏差）** | 失败 + 段落没问题，但 agent 没遵守 | 往执行附录追加提醒 | 仅 `S_app` — **绝不**碰 `S_body` |

最易混淆的边界是 **SkillDefect vs ExecutionLapse**。本技能提供"字面对比法"加以区分，并给出一个一问判定：*"如果 agent 严格按段落执行，任务会成功吗？"* —— 会 → ExecutionLapse；不会 → SkillDefect。

## 为什么需要这个技能

现有的 skill 自演化方法是"skill-unaware"的：把轨迹转化为通用反馈，然后整体重写 skill。EmbodiSkill 证明这会累积冗余内容、覆盖有效指导、保留错误表述。四类分类法正是为解决这个问题而生。

## 何时使用

满足**所有**以下条件时使用：

- 刚完成一个**程序性任务**——指应用了某个具名 skill、方法或多步程序、其结果依赖中间步骤的任务。判定法：agent 是否执行了一个 ≥2 步的有序过程、且结果依赖中间状态？
- 任务中至少用到了一个 skill、子流程或具名程序
- 任务结果可评估：成功、部分成功或失败

**不适用**：单次工具调用、单次信息查询、单步回忆等不含程序性 skill 的任务。

## 安装

```bash
# 方式一：解压打包好的 .skill 文件
unzip skill-aware-reflection.skill -d ~/.claude/skills/

# 方式二：克隆本仓库
git clone https://github.com/z77orz/skill-aware-reflection.git \
    ~/.claude/skills/skill-aware-reflection
```

放置在 `~/.claude/skills/` 下后，Claude Code  会自动发现并按 description 触发。

## 仓库结构

```
skill-aware-reflection/
├── SKILL.md                  # 主体（先读这个）
├── examples.md               # 6 个完整示例，每类一个
├── reflection-record.md      # 反思记录模板
├── evals/
│   └── evals.json            # 4 个标准格式测试 prompt
├── tests/                    # TDD 制品（RED / REFACTOR 阶段产出）
│   ├── pressure-scenarios.md # 6 个压力测试场景
│   ├── baseline-failures.md  # 8 种被本技能拦截的基线失败模式
│   └── verification.md       # 交叉验证：skill 是否覆盖每个场景
├── README.md                 # 英文版说明
├── README.zh.md              # 中文版说明（本文件）
└── LICENSE
```

## 验证结果

针对 4 个 benchmark 评估运行。结论：

| 配置 | 通过率 | 时间 | Tokens |
|---|---|---|---|
| **使用 Skill** | **100%** | 62.3s ± 12.3s | 73,525 |
| 不使用 Skill | 64% | 50.9s ± 5.8s | 69,211 |
| **增益（Delta）** | **+0.36** | +11.5s | +4,314 |

最大鉴别点是 `SkillDefect` 分类 —— 基线 25%（1/4），使用 skill 后 100%（4/4）。没有这个框架时，agent 倾向于把"skill 内容错误"误判为"执行偏差"，或给出笼统的"打补丁"。

复现方式：参考本地开发环境的 `~/.claude/skills/skill-aware-reflection-workspace/` 目录，其中包含 `grade.py` 和 `aggregate_benchmark.py` 脚本。

## 与 EmbodiSkill 论文的对应

| EmbodiSkill 概念 | 本技能中的对应 |
|---|---|
| `c_i`（反思类型）| `type` 字段，4 选 1 |
| `e_i`（轨迹证据）| `evidence` 字段，必填 |
| `d_i`（更新指令）| `directive` 字段，4 种离散动作 |
| `b_i`（目标段落）| `target_skill_content` 字段，verbatim 引用 |
| `S_body` | 主 skill 文档（前 3 类可改）|
| `S_app` | 执行附录（仅 ExecutionLapse 写入）|
| Skill-Aware Evolution Spiral | SKILL.md 中 Quick Algorithm 第 4 步 |

## 引用

```bibtex
@article{ju2026embodiskill,
  title={EmbodiSkill: Skill-Aware Reflection for Self-Evolving Embodied Agents},
  author={Ju, Ruofei and Wang, Xinrui and Ding, Xin and Yang, Yifan and Wu, Hao and Jiang, Shiqi and Zhang, Qianxi and Wen, Hao and Li, Xiangyu and Wang, Meijun and Li, Kun and Liu, Yunxin and Dai, Haipeng and Wang, Wei and Cao, Ting},
  journal={arXiv preprint arXiv:2605.10332},
  year={2026}
}
```

## 许可

MIT
