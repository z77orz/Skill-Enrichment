# Examples: Skill-Aware Reflection

Each example shows a full reflection record for one of the four types. Use these as templates — fill in your own `b_i` quote, evidence, and directive.

> **Reading note**: `b_i` is always shown as a verbatim quoted snippet from the current skill. Empty `b_i` is only valid for DISCOVERY.

---

## Example 1 — DISCOVERY

**Task context**: Used `pdf-processing` skill on a scanned PDF. Task succeeded. Mid-task, the agent had to fall back to OCR + Tesseract because the PDF had no text layer — `pdf-processing` skill's "extract text" paragraph assumes a text layer.

**Trajectory evidence** (quoted from the run):
> ```
> Read tool: page 1 → "image-only, no text layer detected"
> Read tool: page 1 → "no extractable text"
> Bash tool: tesseract page1.png page1 -l chi_sim
> Read tool: page1.txt → "<OCR result>"
> ```

**Decision walk**:
- Outcome r = 1 (success).
- Did the trajectory exercise a procedure the current skill does not cover? **Yes** — OCR fallback for image-only PDFs.
- b_i search: the skill's body has a paragraph "extract text using Read tool" but **no** paragraph on OCR fallback. So this is new, not optimization.

**Reflection record**:
```
[REFLECTION: DISCOVERY]
evidence:
  - "Read tool: image-only, no text layer detected"
  - "Bash tool: tesseract page1.png page1 -l chi_sim"
target_skill_content b_i: (none — new capability not in current skill)
directive: APPEND new paragraph
new_content:
  ## 扫描件 / 图像型 PDF 的文本提取
  当 Read 工具返回 "image-only" 或 "no extractable text" 时，
  改用 OCR 路径：
  1. 调 Bash 工具：`tesseract <page.png> <out> -l chi_sim+eng`
  2. 用 Read 工具读取生成的 .txt 文件
  3. 提取的文本继续进入后续分析流程
```

**Updated S_body**: append the new paragraph at the end of the existing "extract text" section.

---

## Example 2 — OPTIMIZATION

**Task context**: Used `contract-review` skill to review a 30-page NDA. Task succeeded, but took 25 minutes. The skill's body has a paragraph saying "evaluate all 12 risk categories". The agent noticed 3 categories (antitrust, export-control, ESG) were obviously inapplicable to this NDA.

**Trajectory evidence** (quoted from the run):
> ```
> 12:00 — Reviewed antitrust risk: NDA does not involve market allocation, M&A, or pricing → not applicable
> 12:30 — Reviewed export-control risk: NDA is for software training services, no dual-use tech → not applicable
> 13:00 — Reviewed ESG risk: NDA is between two private parties, no public-interest dimension → not applicable
> 13:05 — Reached end of risk evaluation, proceeded to opinion
> ```

**Decision walk**:
- Outcome r = 1 (success).
- Was a new capability exercised? No — the agent stayed within the 12-category procedure.
- Does some b_i have a more efficient form? **Yes** — "evaluate all 12 risk categories" can be made smarter: skip inapplicable ones, with a brief justification.

**Reflection record**:
```
[REFLECTION: OPTIMIZATION]
evidence:
  - "Reviewed antitrust risk: ... not applicable"
  - "Reviewed export-control risk: ... not applicable"
  - "Reviewed ESG risk: ... not applicable"
target_skill_content b_i:
  "按 12 类风险逐条审查（反垄断、出口管制、ESG、劳动、知识产权、
   数据合规、保密、违约责任、争议解决、合同变更、不可抗力、合同终止）。"
directive: REPLACE b_i WITH <new>
new_content:
  "按 12 类风险逐条审查（反垄断、出口管制、ESG、劳动、知识产权、
   数据合规、保密、违约责任、争议解决、合同变更、不可抗力、合同终止）。
   审查时先做适用性初筛：若一类风险与本合同无事实关联（如 NDA 涉及
   反垄断的概率极低），用一句话说明不适用并跳过，记录在审查日志中。
   仅对适用类别展开实质分析。"
```

**Updated S_body**: the old paragraph is replaced with the new one. The 12-category list is preserved (only the procedure is streamlined).

---

## Example 3 — SKILL_DEFECT

**Task context**: Used `feishu-auth` skill to configure a Feishu app. Task failed. The skill's body says to visit `https://open.feishu.cn/auth` for OAuth, but Feishu has migrated the domain to `https://open.larksuite.com/auth`.

**Trajectory evidence** (quoted from the run):
> ```
> Bash tool: curl -I https://open.feishu.cn/auth
>   → HTTP 301 Moved Permanently, Location: https://open.larksuite.com/auth
> Bash tool: curl -I https://open.larksuite.com/auth
>   → HTTP 200 OK
> WebFetch: open.feishu.cn/auth → "this domain has been retired"
> ```

**Decision walk**:
- Outcome r = 0 (failure).
- Quote the relevant b_i: "访问 https://open.feishu.cn/auth 完成 OAuth"
- Quote the actual action sequence: agent tried the URL → got 301 → followed redirect → succeeded at the new URL.
- Apply literal comparison: skill says `open.feishu.cn`, the working URL is `open.larksuite.com`. **The skill's URL is wrong.** Following the skill verbatim would still fail.
- → SKILL_DEFECT (replace the URL).

**Reflection record**:
```
[REFLECTION: SKILL_DEFECT]
evidence:
  - "Bash tool: curl -I https://open.feishu.cn/auth → 301 Moved to larksuite.com"
  - "WebFetch: open.feishu.cn/auth → 'this domain has been retired'"
target_skill_content b_i:
  "步骤 3：访问 https://open.feishu.cn/auth 完成 OAuth 授权。"
directive: REPLACE b_i WITH <new>
new_content:
  "步骤 3：访问 https://open.larksuite.com/auth 完成 OAuth 授权。
  注：飞书国际版与国内版已统一到 larksuite.com 域名，原 feishu.cn
  域名永久重定向到新地址。"
```

**Updated S_body**: the URL is replaced; the rest of the paragraph structure is kept.

---

## Example 4 — EXECUTION_LAPSE

**Task context**: Used `daily-work-log` skill to generate today's work log. Task failed — the log file was created but empty. The skill's body says "before generating, Read the last 5 session messages". The agent skipped that step and called Write directly.

**Trajectory evidence** (quoted from the run):
> ```
> Skill instruction: "before generating, Read the last 5 session messages"
> Agent action: Write("/path/to/log.md", "")   ← no preceding Read
> Result: file created, content empty
> Verification: Read /path/to/log.md → 0 bytes
> ```

**Decision walk**:
- Outcome r = 0 (failure).
- Quote the relevant b_i: "before generating, Read the last 5 session messages"
- Quote the actual action sequence: agent called Write without prior Read.
- Apply literal comparison: skill says "Read first", agent did not Read. **The skill is correct, the agent did not follow it.**
- → EXECUTION_LAPSE. Do NOT modify the body. Append a reminder to S_app.

**Reflection record**:
```
[REFLECTION: EXECUTION_LAPSE]
evidence:
  - "Agent action: Write(/path/to/log.md, '') with no preceding Read"
  - "Skill instruction: 'before generating, Read the last 5 session messages'"
target_skill_content b_i:
  "在生成日志前，使用 Read 工具读取最近 5 条会话消息，作为日志内容源。"
directive: APPEND_TO_APPENDIX <reminder>
new_content:
  【执行提醒】此步骤必须严格按顺序：先 Read → 解析 → 再 Write。
  跳过 Read 直接 Write 会生成空日志。已发生 1 次。
```

**Updated S_app**: append the reminder to the appendix. **S_body is unchanged.**

---

## Example 5 — When NOT to Reflect (no record)

**Task context**: Used `mermaid-visualizer` skill to draw a flowchart. Task succeeded cleanly. The agent thought: "what if we also added support for ER diagrams?". But the user did not ask for ER diagrams, and no trajectory exercised ER diagram generation.

**Decision walk**:
- Outcome r = 1 (success).
- Did the trajectory exercise a procedure the current skill does not cover? **No** — only the flowchart procedure was used.
- Was any `b_i` suboptimal? **No** — flowchart generation worked as expected.
- Was the user's task outside the skill's scope (like ER diagrams)? Yes — but that is a future request, not a present capability.

**Output**:
```
[REFLECTION: NONE]
reason: Trajectory only exercised existing flowchart capability.
        ER-diagram support is a hypothetical future request, not a discovered gap.
        No reflection record emitted; S unchanged.
```

**Important**: Even though "add ER diagram support" sounds like a reasonable improvement, it has no trajectory evidence. Do NOT emit DISCOVERY here. Speculative additions pollute the skill.

---

## Example 6 — Boundary Case: SKILL_DEFECT vs EXECUTION_LAPSE

This is the most error-prone boundary. Two failures, both with valid-looking b_i. The difference is whether **following b_i perfectly would have led to success**.

### Case A → SKILL_DEFECT

**Trajectory**:
> Skill paragraph b_i: "如果 API 返回 500，重试 3 次后放弃。"
> Agent action: retried 3 times, gave up.
> Result: task failed.

Was b_i followed? Yes. Did following it perfectly succeed? No — because retrying is the wrong strategy; the API has a real bug.
→ **SKILL_DEFECT** with directive REPLACE.

### Case B → EXECUTION_LAPSE

**Trajectory**:
> Skill paragraph b_i: "如果 API 返回 500，立即调用 on_error() 钩子记录上下文。"
> Agent action: retried without calling on_error().
> Result: task failed (and on_error() was never logged, so the team lost debugging context).

Was b_i followed? No. Did following b_i perfectly succeed? Yes — on_error() would have logged the context even if the underlying API still failed.
→ **EXECUTION_LAPSE**. Add b_i to S_app as a reminder.

### The One-Question Test

> "If the agent had followed b_i to the letter, would the task have succeeded?"

- **Yes** → EXECUTION_LAPSE (or success, no record needed)
- **No** → SKILL_DEFECT (b_i is wrong/incomplete/underspecified)
- **N/A** (b_i doesn't apply to the situation) → check whether b_i should have been invoked at all; if so, SKILL_DEFECT (incomplete); if not, ExecutionLapse didn't apply either → ESCALATE
