# GitHub 仓库重命名操作清单

> 目标:`https://github.com/z77orz/skill-aware-reflection` → `https://github.com/z77orz/Skill-Enrichment`

## 步骤总览

```
① 浏览器端重命名仓库(0 分钟)
       ↓
② 本地 git 改 remote URL(30 秒)
       ↓
③ push 新提交(原 push + 改名后的 README)
       ↓
④ 验证 + 通知归档
```

---

## 步骤 ① · 浏览器端重命名

1. 打开 <https://github.com/z77orz/skill-aware-reflection/settings>
2. 找到 **Repository name** 字段
3. 把 `skill-aware-reflection` 改成 **`Skill-Enrichment`**
4. 点击 **Rename**
5. GitHub 会自动:
   - 把旧 URL 301 跳转到新 URL(收藏夹不会断)
   - 旧 URL 的 `git clone` 仍可工作
   - 自动跳转到 <https://github.com/z77orz/Skill-Enrichment>

---

## 步骤 ② · 本地改 remote URL

```bash
cd ~/.claude/skills/Skill-Enrichment

# 2.1 验证当前 remote
git remote -v
# 应该是:origin  https://github.com/z77orz/skill-aware-reflection.git

# 2.2 改 URL 到新仓库
git remote set-url origin https://github.com/z77orz/Skill-Enrichment.git

# 2.3 验证
git remote -v
# 应该是:origin  https://github.com/z77orz/Skill-Enrichment.git (fetch)
#          origin  https://github.com/z77orz/Skill-Enrichment.git (push)
```

---

## 步骤 ③ · 提交未提交内容 + push

```bash
cd ~/.claude/skills/Skill-Enrichment

# 3.1 检查当前状态
git status

# 3.2 暂存所有变更(图鉴风 README + 学术声明等)
git add -A

# 3.3 提交
git commit -m "refactor: rebrand to 丰容 / Skill Enrichment

- README/READMEs redesigned in 'Field Guide' aesthetic (园丁手记)
- Stronger academic attribution to EmbodiSkill (Ju et al., 2026)
- 4-type reflection framework operationalized for Claude Code
- Decision tree + needs matrix vs. hermes-agent
- Packaged as Skill-Enrichment.skill"

# 3.4 推送到新仓库
git push -u origin master
```

> **注意**:GitHub 端 rename 后,新仓库继承旧的 commit history。
> 因此第一次 push 不需要 `--force`,直接 push 即可。

---

## 步骤 ④ · 验证清单

```bash
cd ~/.claude/skills/Skill-Enrichment

# 4.1 远程指向新 URL
git remote -v | grep Skill-Enrichment && echo "✅ remote OK"

# 4.2 本地领先/落后远程 0 提交
git status -sb
# 期望:# master...origin/master  (无 ahead/behind)

# 4.3 本地最近 5 提交
git log --oneline -5
```

打开 <https://github.com/z77orz/Skill-Enrichment> 检查:

| 验证项 | 期望 |
|---|---|
| 仓库名 | `z77orz/Skill-Enrichment` |
| About 描述(可选填) | *Skill Enrichment — EmbodiSkill port for Claude Code* |
| README 渲染 | 顶部"✦ 丰容 (Skill Enrichment) ✦" + 园丁手记封面 |
| topics(可选) | `claude-code` `claude-skills` `embodi-skill` `agent` `reflection` |
| Releases(可选) | 上传 `Skill-Enrichment.skill` 作为 v1.0.0 release asset |

---

## 步骤 ⑤ · 后续可选动作

```bash
# 5.1 通知 git 用户(如有协作者)
# GitHub 端 rename 不自动发邮件给协作者,需手动通知

# 5.2 更新引用
# 所有引用 https://github.com/z77orz/skill-aware-reflection 的地方:
#   - 个人笔记 / 博客 / arXiv 评议 / Slack
#   - 替换为 https://github.com/z77orz/Skill-Enrichment

# 5.3 通知论文作者(如已建立联系)
# "我们已将工程化移植项目从 skill-aware-reflection 更名为 Skill-Enrichment,
#  原 URL 会自动重定向到新 URL。"
```

---

## 故障排查

| 现象 | 解决 |
|---|---|
| `git push` 报 403 | 检查 GitHub 端 rename 是否完成(Settings 顶部应显示新名) |
| `git push` 报 "repository not found" | 重新执行步骤 ②.2,确认 URL 大小写完全一致 |
| 旧 URL 打不开 | 正常现象——rename 完成后旧 URL 应 301 到新 URL;若 5 分钟后仍未跳转,刷新浏览器 |
| 找不到 Settings | 确认你登录的是 `z77orz` 账号,不是组织账号 |

---

## 回滚方案(若 rename 后想撤销)

1. 浏览器端:再次进入 Settings,把 `Skill-Enrichment` 改回 `skill-aware-reflection`
2. 本地:`git remote set-url origin https://github.com/z77orz/skill-aware-reflection.git`
3. push:`git push -u origin master`

rename 在 GitHub 上是**可逆的**,不用担心。
