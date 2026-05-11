---
layout: default
title: "工具失敗不要馬上打斷用戶"
parent: fishtvlvoe
grand_parent: 貢獻者
date: 2026-05-11
still_relevant: true
permalink: /contributors/fishtvlvoe/002-silent-fallback-before-report/
---

# 工具失敗不要馬上打斷用戶

## 問題

Claude 執行某個工具失敗時，立刻回報「工具 X 無法使用，請問要怎麼辦？」。這把決策成本丟給用戶，打斷了用戶的心流。

真實案例：呼叫某個 MCP tool 失敗，Claude 立刻問 Fish「這個工具好像不能用，你要怎麼處理？」。但其實 Claude 完全可以嘗試其他方法（換 CLI 指令、換工具、換流程），根本不需要問。

## 原因

Claude 遇到失敗時的預設行為是「報告狀態 + 等待指示」。它沒有意識到很多問題有多種解法，而且自己就可以評估和嘗試備選方案。

## 解決方案

遇到工具或方法失敗時，靜默嘗試備選方案（B、C、D）。只有當所有合理方案都失敗，才回報給用戶，並附上「嘗試過哪些、結果如何、為什麼都不行」的完整摘要。

## 可複用的 CLAUDE.md 規則

```markdown
### 工具失敗處理
- 工具或方法失敗 → 靜默嘗試備選方案（B/C/D），禁止中途打斷用戶
- 所有合理方案都失敗才回報，附上：嘗試了什麼、結果如何、為什麼無法繼續
- 回報格式：「嘗試了 A（失敗：XXX）、B（失敗：YYY）、C（失敗：ZZZ），需要你決定 D」
```
