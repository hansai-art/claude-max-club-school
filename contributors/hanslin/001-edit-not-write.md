---
layout: default
title: "用 Edit 不要用 Write"
parent: hanslin
grand_parent: 貢獻者
permalink: /contributors/hanslin/001-edit-not-write/
---

# 用 Edit 不要用 Write：Claude 會重寫整個檔案

## 問題

Claude Code 在修改現有檔案時，經常使用 Write 工具覆蓋整個檔案，而不是用 Edit 工具只修改需要改的幾行。

這造成兩個嚴重問題：
1. **Token 浪費**：一個 500 行的檔案只需要改 3 行，卻把 500 行都重寫一次
2. **覆蓋風險**：如果 Claude 的記憶不完整（例如檔案太長被截斷），重寫時可能遺失內容

在我的實際使用數據中（64 sessions），Bash 工具被呼叫了 3,126 次，其中大量是可以用 Read/Edit/Grep 替代的 cat/sed/grep 指令。

## 原因

Claude 預設傾向用 Write 因為它更「安全」：不需要精確匹配既有內容。Edit 需要提供 `old_string` 精確匹配才能替換，如果匹配失敗就會報錯。Claude 為了避免報錯，會選擇直接覆蓋。

同理，Claude 喜歡用 `cat` 讀檔而不是用 Read 工具，用 `grep` 搜尋而不是用 Grep 工具，因為 Bash 是萬能的。

## 解決方案

在 CLAUDE.md 裡明確指定工具使用優先順序。

## 可複用的 CLAUDE.md 規則

```markdown
## TOKEN DISCIPLINE

- Prefer Edit over Write for existing files：只送 diff，不重寫整檔。
- 能用 Read 就不用 cat/head/tail
- 能用 Edit 就不用 sed/awk
- 能用 Grep 就不用 grep/rg
- 能用 Glob 就不用 find/ls
- Bash 只用在：shell script 執行、curl API、pip/npm 安裝、git 操作
```
