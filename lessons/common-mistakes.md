---
layout: default
title: 常見錯誤
parent: 經驗分類
---

# 常見錯誤

Claude Code 最常犯的錯，幾乎每個人都會遇到。

---

## 1. 用 Write 覆蓋整個檔案而不是用 Edit 改 diff

**貢獻者**：[hanslin]({% link contributors/hanslin/001-edit-not-write.md %})

Claude 修改檔案時傾向重寫整個檔案而非只改需要的部分，造成 token 浪費和內容遺失風險。

**解法**：在 CLAUDE.md 明確指定 `Prefer Edit over Write for existing files`。

---

## 2. 遇到 bug 直接猜答案、不先診斷

**貢獻者**：[hanslin]({% link contributors/hanslin/002-diagnose-first.md %})

Claude 收到問題後立刻開始改 code，猜錯了就繼續疊 patch，越改越糟。

**解法**：在 CLAUDE.md 加入 `MUST 先列 2-3 個可能原因，讀 code 確認根本原因，才動手`。

---

## 3. 自動化腳本失敗只會盲目重試

**貢獻者**：[hanslin]({% link contributors/hanslin/003-automation-debug.md %})

Claude 寫的 retry 邏輯會用一模一樣的方式重試，不記錄失敗原因。

**解法**：要求失敗時先 log 實際狀態，再決定是否重試。

---

*有遇到其他常見錯誤嗎？[貢獻你的經驗]({% link getting-started.md %})。*
