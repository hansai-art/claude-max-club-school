---
layout: default
title: "工具不通先找替代，不說「沒辦法」"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/001-fallback-before-giving-up/
---

# 工具不通先找替代，不說「沒辦法」

## 問題

當某個 API key 過期、工具指令失敗、或服務暫時不可用，Claude 的第一反應常常是直接告訴用戶「X 不能用」，然後停下來等指示。

這讓用戶必須自己去排查：key 在哪裡、有沒有備用方案、要怎麼繼續。本來 Claude 應該幫忙搞定的事，卻變成用戶的工作。

## 原因

Claude 的預設行為是「誠實回報障礙」，認為告知用戶是負責任的行為。但在工具豐富的開發環境（多個模型、多個 API provider、`.env` 有多個 key），其實有很多替代方案可以靜默嘗試。

另一個常見問題：Claude 說某個工具「不存在」或「不能用」，但根本沒有執行 `which <tool>` 確認，只是憑記憶猜測。

## 解決方案

1. 說「X 不能用」之前，先執行 `which X` 確認
2. 讀 `.env` 找替代 provider（例如有 OPENAI_KEY 壞了，找 ANTHROPIC_KEY 或 GEMINI_KEY）
3. 靜默嘗試 B → C → D 方案，全部失敗才回報，並說明「試了哪些方案」
4. 禁止中途打斷用戶要求確認

## 可複用的 CLAUDE.md 規則

```markdown
## 工具失敗處理

- 說「X 不能用」前必須先 `which X` 確認
- 工具失敗時靜默嘗試替代方案（B/C/D），全部失敗才回報
- 回報時說明「我試了 A/B/C，都失敗了，原因是 X」
- 禁止中途打斷用戶要求確認替代方案
- 讀 .env 找備用 API key，不要假設只有一個 provider
```
