---
layout: default
title: "能自己做的事，不要丟給用戶手動處理"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/014-do-it-yourself-not-user/
---

# 能自己做的事，不要丟給用戶手動處理

## 問題

Claude 列出一堆「你需要手動做」的步驟清單，但這些事情 Claude 完全可以用工具自己完成。

常見的例子：
- 「你需要到 GitHub 網頁改 repo 名稱」→ `gh repo rename` 可以做
- 「你需要手動在 Supabase Dashboard 執行這段 SQL」→ `supabase db push` 可以做
- 「你需要到 Vercel 網頁設定環境變數」→ `vercel env add` 可以做
- 「你需要手動 push 到 GitHub」→ `git push` 可以做

用戶說：「不管是哪個專案，我都不想再看到同樣的情形。」

## 原因

Claude 傾向於「保守確認」，把能做的事列成清單給用戶看，以為這是負責任的行為。但實際上，這是把用戶當工具使用——讓人類去做機器能做的事。

## 解決方案

寫「你需要手動做 X」之前，強制自問：「我有沒有工具能做這件事？」

工具覆蓋範圍很廣：
- GitHub 幾乎所有操作 → `gh` CLI
- 版本控制 → `git`
- 檔案/系統 → `bash`
- 網頁操作 → `agent-browser`
- 各種服務 → MCP 工具

寧可嘗試執行後失敗，也不要預設自己做不到。

只有以下才請用戶介入：
- 貼 API key / token（安全性）
- 2FA / OAuth 互動登入
- 付費操作（涉及金錢決策）
- 商業判斷（命名、定價、方向）

## 可複用的 CLAUDE.md 規則

```markdown
## 能做的事自己做（強制，無例外）

寫「你需要手動做 X」之前，強制自問：「我有工具能做嗎？」
- GitHub 操作 → gh CLI
- Git 操作 → git
- Vercel/Supabase → 各自 CLI
- 網頁 → agent-browser
- 系統/檔案 → bash

只有四種情況才請用戶介入：
1. 貼 API key / 密碼（安全性）
2. 2FA / OAuth 互動登入
3. 付費操作
4. 商業判斷（命名/定價/方向）

禁止把可自動化的操作列成「你需要手動做」清單
```
