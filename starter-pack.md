---
layout: default
title: 新手懶人包 — Claude Code CLAUDE.md 通用規則
nav_order: 3
description: "不管什麼技術棧都適用的 CLAUDE.md 規則懶人包。一鍵安裝，讓你的 Claude Code 立刻變聰明。社群驗證、持續更新。"
permalink: /starter-pack/
---

# 新手懶人包
{: .fs-8 }

不管你用什麼技術棧，這些規則都值得裝。
{: .fs-5 .fw-300 }

由社群投票選出、跨領域通用的 CLAUDE.md 規則。直接全部複製貼進你的 `~/.claude/CLAUDE.md` 就好。

---

## 一鍵安裝

把下面這段話貼給你的 Claude Code：

```
讀取 https://github.com/hansai-art/claude-max-club-school/blob/main/starter-pack.md
把裡面「完整懶人包」區塊的規則加進我的 ~/.claude/CLAUDE.md
如果已經有類似的規則就跳過，不要重複
```

---

## 完整懶人包

```markdown
## 工具使用

- Prefer Edit over Write for existing files — 只送 diff，不重寫整檔
- 能用 Read 就不用 cat/head/tail
- 能用 Edit 就不用 sed/awk
- 能用 Grep 就不用 grep/rg
- 能用 Glob 就不用 find/ls
- Bash 只用在：shell script 執行、curl API、安裝套件、git 操作

## 問題排查

- MUST 先列 2-3 個可能原因，讀 code 確認根本原因，才動手修
- 修法不 work 就 STOP 重新診斷，NEVER 在錯的方向疊 patch
- 失敗後先讀錯誤訊息，不要盲目重試

## 安全與覆蓋保護

- MUST ls before deleting any directory
- 修改已發布的內容前，MUST 先從 API 拉取最新版本
- NEVER 用本地舊檔案覆蓋線上內容
- MUST 遞增版本號，NEVER 覆蓋舊版檔案
- NEVER 未經確認 force push
- NEVER 叫使用者去 Dashboard 執行 SQL，自己找替代方案

## 驗證

- CSS/HTML 變更後，MUST fetch 頁面確認關鍵元素存在且可見
- 上傳內容到任何平台後，MUST 用 API 回讀驗證所有必填欄位
- NEVER 直接說「完成」除非你已經驗證結果

## 效率

- 大檔案（>100 行）先用 Grep 定位行號，再用 Read offset/limit 只讀需要的段落
- 需要讀多個檔案時，一次送多個 Read，不要分多輪
- Write/Edit 完不要 Read 回來驗證，信任自己剛寫的內容

## 自動化腳本

- 偵測失敗時 MUST 先記錄實際狀態到 log，再決定是否重試
- Log 要記「期望值」和「實際值」
- NEVER 用同樣的邏輯盲目 retry

## 回應風格

- 直接講重點，不要開場白和結尾客套話
- 回答完就停，不加「還需要什麼嗎？」
```

各規則的詳細說明和來源在[效率規則]({% link snippets/efficiency.md %})和[安全規則]({% link snippets/safety.md %})。

---

*覺得某條規則應該加入懶人包？[發 PR](https://github.com/hansai-art/claude-max-club-school/pulls) 更新這個頁面。*
