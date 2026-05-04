---
layout: default
title: "說『工具不能用』前先 which X 確認"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [診斷不足, CLAUDE.md規則]
date: 2026-05-04
still_relevant: true
permalink: /contributors/fishtvlvoe/001-verify-tool-availability/
---

# 說「工具不能用」前先 `which X` 確認

## 問題

要求 Claude 使用某個 CLI 工具（例如 `copilot`、`gemini`、`cursor`）時，Claude 直接回答「這個工具在這個環境裡沒有安裝，無法使用」，但實際上工具明明在系統 PATH 裡。

Claude 就這樣放棄了一個完全可用的工具，或叫用戶自己去安裝，浪費時間。

## 原因

Claude 對工具是否存在有訓練期的「印象」，會根據過去的知識推斷某工具「通常不會有」，而沒有實際去查詢系統狀態。缺乏現場驗證的習慣。

## 解決方案

在宣稱任何工具「不能用」之前，必須先執行 `which <工具名>` 確認。如果 `which` 返回路徑，工具就是可用的，直接使用。如果 `which` 確認不存在，才能說不能用，並提供替代方案。

## 可複用的 CLAUDE.md 規則

```markdown
## 工具可用性
- 說「X 不能用」前必須先 `which X` 確認
- which 返回路徑 = 工具可用，直接使用，不要叫用戶安裝
- 禁止根據「印象」推斷工具不存在，要看實際系統狀態
```
