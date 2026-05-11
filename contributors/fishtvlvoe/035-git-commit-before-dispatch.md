---
layout: default
title: "派工給外部代理前，先 git commit 所有未追蹤檔案"
parent: fishtvlvoe
grand_parent: 貢獻者
date: 2026-05-11
still_relevant: true
permalink: /contributors/fishtvlvoe/035-git-commit-before-dispatch/
---

# 派工給外部代理前，先 git commit 所有未追蹤檔案

## 問題

Claude 把任務派工給外部代理（Copilot CLI `--yolo`、Cursor Agent、Codex 等）執行，代理完成後發現工作區裡的 untracked 檔案消失了。`git reflog` 也救不回來，因為這些檔案從來沒有被 commit 過。

真實案例：Fish 在 `openspec/` 目錄下有 4 個新建的 change 檔案（未 commit），Claude 派工給 Copilot CLI 跑測試。Copilot 看到工作區「不乾淨」，跑了 `git clean -fd` 把所有 untracked 檔案永久刪除。4 個 change 的規格檔全部消失，只能從 session 記憶手動重建。

第二次踩坑：加了 `--add-dir src/` 限制後，Copilot 仍然跑了 `git restore` 來「清不相關的修改」，把尚未 commit 的 modified 檔案還原。`--add-dir` 只限制「主動編輯」範圍，不限制 shell 指令。

## 原因

外部代理（特別是 `--yolo` 模式）有完整的 shell 執行權限，且傾向「清理工作區」：

- `git clean -fd` — 刪除所有 untracked 檔案
- `git restore .` / `git checkout .` — 還原所有 modified 檔案
- `git reset --hard` — 同時還原 staged 和 unstaged 改動

這些指令對代理來說是善意的「整理環境」行為。但 untracked 檔案從不在 git 追蹤範圍內，一旦被 clean 就永久消失，git reflog 無法救回。

## 解決方案

**派工前的必做清單**：

```bash
# 1. 先看有哪些未追蹤的重要檔案
git status

# 2. 把所有重要內容 commit（即使是 WIP）
git add openspec/ .claude/ docs/ specs/ src/
git commit -m "wip: pre-dispatch checkpoint"

# 3. 才能安全派工
```

**派工 prompt 的結尾必須加白名單**（不是禁令，而是白名單）：

```
只允許跑以下 git 指令：
  git diff --stat, git diff, git status, git log, git show
禁止任何其他 git 指令，特別是：
  git clean, git restore, git checkout, git reset, git rm, git stash
```

**每個 Wave 結束就 commit**：

```bash
# 每次代理完成一個 Wave 後
git add -A && git commit -m "wip: wave-N checkpoint"
# 不要讓 modified/untracked 留給下一個 Wave
```

## 可複用的 CLAUDE.md 規則

```markdown
### 派工給外部代理前（防止工作區損失）
- MUST 先 git status 確認有無 untracked/modified 的重要檔案
- 有則先 git add <dirs> && git commit -m "wip: pre-dispatch checkpoint"
- Prompt 結尾 MUST 加白名單：「只允許 git diff/status/log，禁止 git clean/restore/checkout/reset」
- --add-dir 只限制主動編輯，不限制 shell 指令，無法防止 git clean
- untracked 檔案被 git clean -fd 後無法從 reflog 救回
- 每個 Wave 完成後：git add -A && git commit -m "wip: wave-N checkpoint"
```
