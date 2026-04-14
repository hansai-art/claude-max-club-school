---
layout: default
title: "改 CSS 沒檢查對比度"
parent: hanslin
grand_parent: 貢獻者
tags: [診斷不足, CLAUDE.md規則]
date: 2026-04-14
still_relevant: true
permalink: /contributors/hanslin/015-contrast-check/
---

# 改 CSS 沒檢查對比度

## 問題

改了一個 CSS 屬性（例如背景色），沒有同步確認文字色在新背景上是否可讀。結果出現白底白字、黑底黑字、白底橘字等看不清的組合。

同一個 session 裡反覆出現這個問題超過 5 次。

## 原因

Claude 每次只專注在「修某個元素的某個屬性」，沒有系統性檢查該元素在所有模式下的完整顯示效果。

## 解決方案

改 CSS 前先列表格。

## 可複用的 CLAUDE.md 規則

```markdown
### CSS 對比度
- 改任何 CSS 前，列出所有受影響元素的「背景色 + 文字色」
- 分別檢查淺色模式和深色模式
- 白底 MUST 配黑字（#000），深色底 MUST 配淺字（#e0ddd5+）
- 不確定的時候，先 curl 線上 theme CSS 查原始值
```
