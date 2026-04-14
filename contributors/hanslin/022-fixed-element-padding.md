---
layout: default
title: "給 fixed 元素留 padding 但它不佔空間"
parent: hanslin
grand_parent: 貢獻者
tags: [診斷不足, CLAUDE.md規則]
date: 2026-04-14
still_relevant: true
permalink: /contributors/hanslin/022-fixed-element-padding/
---

# 給 fixed 元素留 padding 但它不佔空間

## 問題

深色切換按鈕用 `position: fixed` 放在右上角。為了不擋住搜尋框，給 header 加了 `padding-right: 60px`。結果搜尋框右邊出現一大塊空白，因為 fixed 元素脫離文檔流，根本不需要留空間。

## 原因

Claude 混淆了 `position: fixed`（脫離文檔流）和 `position: relative/absolute`（佔據文檔流）。

## 解決方案

```markdown
### CSS 定位
- position: fixed 元素不佔文檔流空間，不需要給其他元素留 padding
- 只有 position: relative 和 static 的元素才佔空間
```
