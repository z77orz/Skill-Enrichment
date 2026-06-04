<div align="right">

<a href="./README.md">English</a> · <a href="https://arxiv.org/abs/2605.10332v1">arXiv</a> · <a href="./CITATION.cff">Cite</a>

</div>

<img src="https://capsule-render.vercel.app/api?type=rect&height=4&color=3F5D3A&text=&fontSize=0" width="100%" alt=""/>

<!-- ============================================================
     HERO · 园丁手记封面
     ============================================================ -->
<div align="center">

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/h1.svg" alt="丰容 Skill Enrichment" height="110"/>

<br/>

<a href="https://arxiv.org/abs/2605.10332v1"><img src="https://img.shields.io/badge/MIT-开源-3F5D3A?style=flat-square&logo=opensourceinitiative&logoColor=white" alt="MIT"/></a>
<a href="https://www.anthropic.com/claude-code"><img src="https://img.shields.io/badge/Claude_Code-技能-A3541E?style=flat-square&logo=anthropic&logoColor=white" alt="Claude Code"/></a>
<a href="https://arxiv.org/abs/2605.10332v1"><img src="https://img.shields.io/badge/EmbodiSkill-arXiv-3F5D3A?style=flat-square&logo=arxiv&logoColor=white" alt="arXiv"/></a>
<a href="./CITATION.cff"><img src="https://img.shields.io/badge/Cite-CFF-A87C2C?style=flat-square" alt="Cite"/></a>

<br/>

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/typing-zh.svg" alt="Typing SVG" width="900"/>

<br/>

<table>
<tr>
<td align="center" width="33%">

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/card-zh-1.svg" alt="被丰容者" height="32"/><br/>
<i>程序性 skill</i>

</td>
<td align="center" width="33%">

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/card-zh-2.svg" alt="核心营养" height="32"/><br/>
<i>任务轨迹</i>

</td>
<td align="center" width="33%">

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/card-zh-3.svg" alt="终局" height="32"/><br/>
<i>成熟化 · 0 → 1</i>

</td>
</tr>
</table>

</div>

<br/>
<div align="center">

[📖 快速开始](#快速开始) · [🔧 工作机制](#工作机制) · [📂 仓库结构](#仓库结构) · [📊 验证](#验证)

</div>

---

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/h2-zh-xue-ming-ka.svg" alt="学名卡" height="42"/>

<table>
<tr><th align="left" width="22%">字段</th><th align="left">内容</th></tr>
<tr><td><b>俗名</b></td><td><b>丰容 / Skill Enrichment</b></td></tr>
<tr><td><b>曾用名</b></td><td><i>Skill-Aware Reflection</i>（原仓库 skill-aware-reflection）</td></tr>
<tr><td><b>科属</b></td><td>EmbodiSkill — <i>自演化具身智能体</i></td></tr>
<tr><td><b>模式产地</b></td><td>Ju et al., 2026 · arXiv:2605.10332v1 · <a href="https://arxiv.org/abs/2605.10332v1">链接</a></td></tr>
<tr><td><b>栖息地</b></td><td><code>~/.claude/skills/Skill-Enrichment/</code></td></tr>
<tr><td><b>食性</b></td><td>真实任务轨迹（即<b>核心营养</b>）</td></tr>
<tr><td><b>饲养员</b></td><td>agent 自身，在四类反思框架下作业</td></tr>
<tr><td><b>保护级别</b></td><td>

`MIT` — 开源 · `arXiv preprint` — 学术引用强制

</td></tr>
</table>

---

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/h2-zh-guan-yu-ming-ming.svg" alt="关于命名" height="42"/>

> *在动物福利科学中，**环境丰容（Environmental Enrichment）** 是一种实践——为圈养动物提供多样化、具有生物学意义的环境刺激，满足其生理与心理需求，促进行为表达的自然化，减少刻板行为。*
>
> *本项目字面化地借用这一概念。*

| 域 | 圈养环境（动物福利） | Claude Code（本项目） |
|---|---|---|
| 被丰容者 | 圈养动物 | 程序性 skill |
| 丰容刺激 | 多样化环境 | 真实任务轨迹 |
| 促进行为 | 自然行为展示 | 跨场景适用的程序性能力 |
| 需避免 | 刻板行为（stereotypy） | 把同一个过时的做法，不加辨别地套到每个新任务上 |
| 丰容执行者 | 动物园管理员（zookeeper） | agent（在四类反思框架下） |

这个比喻不是装饰，而是项目组织原则：

> <b>没有轨迹，就没有丰容。</b> 一段从未经历真实运行的 skill，永远长不大。

### 名字里装着什么

| 名词 | 角色 |
|---|---|
| **EmbodiSkill** | 论文框架名 |
| **Skill-Aware Reflection** | 论文中子方法名 |
| **丰容 / Skill Enrichment** | 本工程化项目名——命名「刺激→成熟」整体过程 |

---

<table>
<tr><td>

> ### ⟁ 学术来源声明
>
> 本 skill <b>不是独立原创方法</b>，而是论文 EmbodiSkill 的工程化移植。
>
> 核心方法论（四类反思、`S_body`/`S_app` 结构、分类逻辑）由论文作者 Ju et al. (2026, arXiv:2605.10332) 提出。
>
> 本仓库的工程化贡献见 [`SKILL.md`](./SKILL.md)。
>
> <b>使用本 skill 即视为同意</b>：若在学术或商业场景中引用本 skill，需同时引用原论文。

</td></tr>
</table>

---

## 快速开始

### 安装

```bash
# 方式一：解压打包好的 .skill 文件
unzip Skill-Enrichment.skill -d ~/.claude/skills/

# 方式二：克隆本仓库
git clone https://github.com/z77orz/Skill-Enrichment.git \
    ~/.claude/skills/Skill-Enrichment
```

放置在 `~/.claude/skills/Skill-Enrichment/` 下后，Claude Code 会自动发现并按 description 触发。

### 使用

在 Claude Code 中，说以下任一触发词即可启动：

| 类型 | 触发词示例 |
|---|---|
| 主触发词 | 「反思技能」「进化技能」「优化技能」 |
| 衍生同义 | 「复盘技能」「丰容技能」「技能复盘」 |
| 英文等价 | 「reflect on skill」「evolve skill」「optimize skill」 |

**典型使用场景**：

```
你：反思技能，今天跑了好几个 skill，有的快有的慢，想整体看看。

→ 丰容扫描当前会话，列出已执行任务让您挑选
→ 您选择 (任务, skill) 组合
→ 生成 reflection record 草稿给您审阅
→ 您确认后才修改 SKILL.md
```

**完整管线**（6 步）：

```text
Step 0: Trigger Verification  ←─ description 语义召回 + Step 0 机械精确匹配
   │
   ▼
Step 1: Task Inventory        ←─ 扫描会话提取 (任务, skill) 列表
   │
   ▼
Step 2: User Selection        ←─ 您挑选要反思的组合
   │
   ├─ 同一 skill ≥ 2 次? → Step 2.5: 逐个 vs 聚合
   │
   ▼
Step 3: Generate Record       ←─ 四类分类 (Discovery/Optimization/SkillDefect/ExecutionLapse)
   │
   ▼
Step 4: Confirmation Gate     ←─ 给您审阅，不直接改文件
   │   ├─ 采纳 → Step 5
   │   ├─ 拒绝 → 写日志 (rejected)
   │   └─ 修改 → 重生成
   │
   ▼
Step 5: Safety Check + Edit   ←─ b_i 唯一性 / 改后 ≤ 50% / directive 枚举校验
   │
   ▼
Audit Log                     ←─ 记录到 reflections/YYYY-MM-DD.md
```

---

## 工作机制

每完成一个**程序性任务**后（指应用了某个具名 skill、流程或多步程序、其结果依赖中间步骤的任务），丰容引导 agent 把「刚才发生了什么」归入**四种类型**之一，并对底层 skill 做出**有针对性的、非破坏性的**修订——绝不整体重写。

### 四类反思

<table>
<tr><th width="14%">动物</th><th width="18%">类型</th><th width="24%">触发条件</th><th width="24%">动作</th><th width="20%">修改对象</th></tr>
<tr><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/animal-fox.svg" alt="fox" width="100"/></td><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/chip-discovery.svg" alt="Discovery" height="64"/></td><td>成功 + 出现 skill 未覆盖的新能力</td><td>记录新 skill 种子</td><td><code>S_body</code>（追加）</td></tr>
<tr><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/animal-bird.svg" alt="bird" width="100"/></td><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/chip-optimization.svg" alt="Optimization" height="64"/></td><td>成功 + 现有段落有更优形式</td><td>替换或补全目标段落</td><td><code>S_body</code>（替换/补全）</td></tr>
<tr><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/animal-tree.svg" alt="tree" width="100"/></td><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/chip-skilldefect.svg" alt="SkillDefect" height="64"/></td><td>失败 + 段落本身错误、不完整或未明确</td><td>替换或补全目标段落</td><td><code>S_body</code>（替换/补全）</td></tr>
<tr><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/animal-octopus.svg" alt="octopus" width="100"/></td><td align="center"><img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/chip-executionlapse.svg" alt="ExecutionLapse" height="64"/></td><td>失败 + 段落没问题，但 agent 没遵守</td><td>往执行附录追加提醒</td><td>仅 <code>S_app</code>——<b>绝不</b>碰 <code>S_body</code></td></tr>
</table>

### 一问判定

> *「如果 agent 严格按段落执行，任务会成功吗？」*
>
> * 会 → **ExecutionLapse**
> * 不会 → **SkillDefect**
>
> 最易混淆的边界是 `SkillDefect ↔ ExecutionLapse`。本技能提供[字面对比法](./examples.md#example-6)加以区分。

---

## 仓库结构

```text
Skill-Enrichment/
├── SKILL.md                  # 主体（267 行，优化版 — 先读这个）
├── examples.md               # 6 个完整示例，每类一个
├── reflection-record.md      # 反思记录模板
├── evals/
│   └── evals.json            # 20 个 trigger 评估 prompt
├── tests/                    # TDD 制品（RED / REFACTOR 阶段产出）
│   ├── pressure-scenarios.md
│   ├── baseline-failures.md
│   └── verification.md
├── assets/                   # Field Guide SVG 资源
├── README.md                 # 英文版说明
├── README.zh.md              # 中文版说明（本文件）
├── CHANGELOG.md              # description 变更历史
├── SPEC-user-trigger.md      # v2 PRD 文档
├── CITATION.cff
└── LICENSE
```

---

## 验证

针对 20 个 trigger eval prompt 运行（详见 [`evals/evals.json`](./evals/evals.json)）。

| 配置 | 通过率 | 时间 | Tokens |
|---|---|---|---|
| **使用 Skill** | **100 %** | 62.3 s ± 12.3 s | 73,525 |
| 不使用 Skill | 64 % | 50.9 s ± 5.8 s | 69,211 |
| **增益（Delta）** | **+0.36** | +11.5 s | +4,314 |

**最大鉴别点**：`SkillDefect` 分类——基线 **25 %**（1/4），使用 skill 后 **100 %**（4/4）。没有这个框架时，agent 倾向于把「skill 内容错误」误判为「执行偏差」，或给出笼统的「打补丁」。

### v2 优化效果

| 指标 | v1（被动触发） | v2（用户主动触发） | v2 优化版（当前） |
|---|---|---|---|
| 触发召回率 | 0% | 39% | 优化中（≤250 字描述测试中） |
| SKILL.md 行数 | 464 | 499 | **267**（−46.5%） |
| 第一阶段动作 | 自动判定 | 用户显式触发词 | 同 v2，更精确 |

---

## 引用

如果在研究或撰写论文时使用了本 skill，请同时引用原始 EmbodiSkill 论文（arXiv 预印本，尚未经过同行评审）：

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

**正文引用形式**：
* 括号式：`(Ju et al., 2026, arXiv:2605.10332)`
* 叙事式：`Ju et al. (2026, arXiv:2605.10332)`

（arXiv ID 为论文永久标识符，目前无期刊 DOI。）

---

## 许可

`MIT`——见 [`LICENSE`](./LICENSE)。MIT 许可适用于本工程化移植；底层方法论仍归 EmbodiSkill 论文作者所有。

<br/>

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=rect&height=2&color=3F5D3A&text=&fontSize=0" width="100%" alt=""/>

<br/>

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/h2-zh-cang-ku-huo-yue-du.svg" alt="仓库活跃度" height="32"/>

<br/>

<img src="https://github-readme-activity-graph.vercel.app/graph?username=z77orz&theme=github-compact&hide_border=true&area=true&bg_color=FAF7F0&color=3F5D3A&line=A3541E&point=A87C2C&hide_title=false" alt="活跃度图" width="92%"/>

</div>

---

<div align="center">

<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/footer-star-moss.svg" alt="✦" height="40"/> 本 README 采用 <i>Field Guide</i>（园丁手记）美学——向 19 世纪博物学家野外图鉴传统致敬。<img src="https://raw.githubusercontent.com/z77orz/Skill-Enrichment/master/assets/footer-star-moss.svg" alt="✦" height="40"/>

<br/>

<sub>为 GitHub Markdown 渲染设计。浅色模式下效果最佳。</sub>

</div>
