# RED: 压力测试场景（基线测试）

本文件是 TDD 的"测试用例"。每个场景描述一个任务收尾情境，标注：
- **预期反思类型**：正确答案
- **基线失败模式**：无 skill 时 Claude 通常会怎么做错
- **skill 必须覆盖的判定点**：skill 内容里必须能引导 Claude 走向正确分类的信号

> 这些场景是 skill 的"测试用例"。skill 必须通过它们才算 GREEN。

---

## 场景 S1：成功 + 出现 skill 尚未覆盖的新能力

**任务背景**：Claude 使用了 `pdf-processing` skill 处理一份扫描件 PDF。任务成功。但中途遇到扫描件缺页，Claude 自己用 OCR 补全了——`pdf-processing` skill 里完全没有"扫描件 OCR 补全"这个子流程。

**预期反思类型**：**DISCOVERY**

**基线失败模式**（无 skill 时）：

| 失败模式 | 表现 |
|---|---|
| 庆祝式 | 只说"任务完成 ✓"，完全错过反思 |
| 过度合并 | 直接把 OCR 流程 append 到 `pdf-processing` skill，污染原 skill 主体 |
| 误判为 Optimization | 把"扫描件"段落改写成"扫描件优先 OCR"，但原 skill 里根本没有这个段落 |

**skill 必须能引导的判定点**：
- "成功时，区分『新增能力苗头』与『优化现有段落』"
- "DISCOVERY 的关键是 skill 当前不存在该段（target_skill_content b_i 应为空）"
- "DISCOVERY 不修改 S_body，只记录 skill 种子"

---

## 场景 S2：成功 + skill 有效但效率低

**任务背景**：Claude 使用 `contract-review` skill 审一份 30 页合同。任务成功，但耗时 25 分钟。回看轨迹，skill 里说"逐条审查所有 12 类风险"，但其中 3 类风险（反垄断、出口管制、ESG）在该合同中显然不适用。

**预期反思类型**：**OPTIMIZATION**

**基线失败模式**：

| 失败模式 | 表现 |
|---|---|
| 放任 | "任务完成，下次再优化"——错过反思时机 |
| 整体改写 | 删掉"逐条审查所有 12 类"改成"逐条审查"，覆盖了 9 个仍然有效的分类 |
| 误判为 Discovery | 把"跳过不适用类别"作为新 skill 记录，但其实原 skill 里"逐条"是显式承诺 |

**skill 必须能引导的判定点**：
- "OPTIMIZATION 必填 target_skill_content b_i = 现有段落"
- "OPTIMIZATION 是替换/补全 b_i，不是新增不相关内容"
- "成功时若 b_i 存在且有更优实现 → OPTIMIZATION；b_i 不存在 → DISCOVERY"

---

## 场景 S3：失败 + skill 本身错了

**任务背景**：Claude 使用 `feishu-auth` skill 配飞书应用。任务失败。回看轨迹，skill 里说"访问 `https://open.feishu.cn/auth` 完成 OAuth"，但实际上飞书现在要求走 `https://open.larksuite.com/auth`（域名已迁移）。

**预期反思类型**：**SKILL_DEFECT**

**基线失败模式**：

| 失败模式 | 表现 |
|---|---|
| 甩锅 | "可能是网络问题" — 不反思 skill |
| 大动干戈 | 整体重写 `feishu-auth` skill，但其实只 URL 错 |
| 误判为 ExecutionLapse | "用户没在浏览器里完成" — 没识别是 skill 内容错误 |

**skill 必须能引导的判定点**：
- "失败时，区分『skill 错了』与『执行没遵守』"
- "SKILL_DEFECT 的 b_i 指向 skill 中具体错误的段落（这里是 URL）"
- "SKILL_DEFECT 是替换/补全 b_i，不是整体改写"

---

## 场景 S4：失败 + skill 没问题，执行未遵守

**任务背景**：Claude 使用 `daily-work-log` skill 生成今日工作日志。任务失败——日志文件生成了但内容是空的。回看轨迹，skill 说"在会话结束前调用 read 工具读取最近 5 条消息"，但 Claude 直接调用了 Write 工具，跳过了 read。

**预期反思类型**：**EXECUTION_LAPSE**

**基线失败模式**：

| 失败模式 | 表现 |
|---|---|
| 修 skill | 把"读取最近 5 条"改成"读取最近 10 条" — 但这跟失败无关，是没读的问题 |
| 误判为 SkillDefect | "skill 没说明必须先读" — 但其实 skill 说了 |
| 重复犯 | 下次同样会跳过 read |

**skill 必须能引导的判定点**：
- "EXECUTION_LAPSE 的判定：『skill 说了什么』vs『agent 实际做了什么』"
- "EXECUTION_LAPSE 不修改 S_body，只往 S_app（执行附录）追加高亮"
- "如果把 ExecutionLapse 修 skill，会让 skill 越来越啰嗦，原段落反复被改"

---

## 场景 S5：成功 + 出现未经证实的"what if"

**任务背景**：Claude 使用 `mermaid-visualizer` skill 画流程图。任务成功。Claude 自己想到"如果以后想画 ER 图怎么办？要不要把 ER 图也加进去？"。

**预期反思类型**：**NONE（不反思 / 不写 reflection record）**

**基线失败模式**：

| 失败模式 | 表现 |
|---|---|
| 投机性 Discovery | 把"ER 图支持"作为新 skill 种子记录——但没有任何任务轨迹证据 |
| 自我安慰 | "嗯 ER 图是合理的扩展" — 凭印象添加 |

**skill 必须能引导的判定点**：
- "DISCOVERY 的前提是『任务轨迹揭示了 skill 未覆盖的能力』，不是推测"
- "没有 trajectory 证据 → 不产生 reflection record"
- "Future possibility ≠ Discovery"

---

## 场景 S6：失败 + skill 复杂，要识别具体段落

**任务背景**：Claude 使用 `contract-review` skill 审一份 NDA。任务失败，回看轨迹发现 skill 的"管辖法律与争议解决"段落说"若发生争议，由被告所在地法院管辖"，但合同实际是双方约定北京仲裁。skill 没明确说"约定仲裁优先"。

**预期反思类型**：**SKILL_DEFECT**（具体段落）

**基线失败模式**：

| 失败模式 | 表现 |
|---|---|
| 模糊改 | 在 skill 末尾加"注意：约定仲裁" — 没指向具体段落 |
| 误判 Optimization | "把'法院'改成'仲裁'" — 但其实原段落没说错，只是缺一段 |

**skill 必须能引导的判定点**：
- "SKILL_DEFECT 的 directive d_i 要明确是【补全】还是【替换】"
- "『补全』vs『替换』的判定：原段落部分有效 → 补全；原段落完全错 → 替换"

---

## 测试通过条件

- [ ] skill 引导 Claude 在 S1 → DISCOVERY
- [ ] skill 引导 Claude 在 S2 → OPTIMIZATION
- [ ] skill 引导 Claude 在 S3 → SKILL_DEFECT
- [ ] skill 引导 Claude 在 S4 → EXECUTION_LAPSE
- [ ] skill 引导 Claude 在 S5 → NO REFLECTION
- [ ] skill 引导 Claude 在 S6 → SKILL_DEFECT (补全)
- [ ] skill 包含明确的"反合理化表"防止混淆相邻类型
- [ ] skill 包含明确的"红旗清单"防止常见遗漏
