---
layout: default
title: "不要用本地舊檔覆蓋遠端內容"
parent: hanslin
grand_parent: 貢獻者
tags: [覆蓋風險, CLAUDE.md規則]
date: 2026-03-15
still_relevant: true
permalink: /contributors/hanslin/005-no-overwrite-remote/
---

# 不要用本地舊檔覆蓋遠端內容

## 問題

Claude 修改 WordPress 文章時，會直接用本地存的舊版 HTML 去覆蓋線上版本。但使用者可能已經在 WordPress 後台手動做了修改（拆段落、改標點、加 highlight、刪整段），這些修改全部被覆蓋消失。

真實案例：一篇 Claude Code Obsidian 文章（Post 1510），使用者在後台花了 30 分鐘手動調整段落結構和 highlight，Claude 用本地舊檔推上去，所有修改全部消失。

## 原因

Claude 不知道「線上版本可能跟本地版本不同」。它只看到本地有一個檔案，就直接拿去用了。

## 解決方案

強制「先拉再改」的工作流程。

## 可複用的 CLAUDE.md 規則

```markdown
### 外部內容修改
- 修改已發布的內容前，MUST 先從 API 拉取最新版本
- NEVER 用本地舊檔案覆蓋線上內容
- 流程：拉取最新 → 在最新版本上修改 → 推回
```
