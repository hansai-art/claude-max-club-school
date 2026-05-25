---
layout: default
title: "需要 API Key 先查 .env，不要問用戶"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/044-check-env-first/
---

# 需要 API Key 先查 .env，不要問用戶

## 問題

Claude 需要呼叫外部 API 時，會問：「請問這個服務的 API Key 是什麼？」或「你有這個服務的 token 嗎？」

但大多數情況下，這些金鑰已經存在 `.env` 或 `.env.local` 裡，根本不需要用戶介入。

## 原因

Claude 沒有主動查詢環境設定的習慣，預設把「取得認證資訊」視為需要用戶提供的輸入。這是 L020（不確定自己查）的具體化，但在 API key 這個情境特別高頻，值得單獨說明。

## 解決方案

任何「這個 API 的 key 是什麼？」問題，MUST 先自查：

```bash
cat .env
cat .env.local
cat .env.production
```

找到就直接用；找不到才問，且問的時候說「已查 .env（和 .env.local），沒有找到 `X_API_KEY`」。

## 可複用的 CLAUDE.md 規則

```markdown
### API 金鑰取得流程
- 需要 API key/token/endpoint 時，MUST 先查：
  - .env
  - .env.local
  - .env.production
- 找到就直接用，NEVER 先問用戶「你有這個服務的 key 嗎」
- 找不到才問，且說明「已查 .env，沒有找到 [KEY_NAME]」
- 這是 L020 的具體化：禁止把自己能查的事丟給用戶
```
