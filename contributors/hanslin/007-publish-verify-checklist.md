---
layout: default
title: "發布前必須 API 回讀驗證"
parent: hanslin
grand_parent: 貢獻者
tags: [盲目重試, 工作流程]
date: 2026-04-02
still_relevant: true
---

# 發布前必須 API 回讀驗證

## 問題

Claude 上傳 WordPress 草稿後，憑記憶認為所有欄位都已設定完成，直接回報「完成」。但實際上漏掉了標籤（tags）和手動摘要（excerpt）。

真實案例：發布 AI PC 文章（Draft 810），只設了分類和 Rank Math SEO，完全漏掉標籤和摘要。

## 原因

發布流程有很多步驟（標題、分類、標籤、摘要、SEO 標題、SEO 描述、特色圖片、slug），Claude 容易漏掉其中幾項，尤其是在長 session 中 context 被壓縮之後。

## 解決方案

上傳草稿後，強制用 API 回讀該文章，逐項檢查所有欄位。

## 可複用的 CLAUDE.md 規則

```markdown
### 發布驗證
- 上傳內容到任何平台後，MUST 用 API 回讀驗證所有必填欄位
- 驗證項目：標題、分類、標籤、摘要、SEO 設定、特色圖片、slug
- 任何一項缺漏就當場補上，不要回報「完成」
```
