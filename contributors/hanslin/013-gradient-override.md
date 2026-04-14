---
layout: default
title: "background-color 蓋不掉 gradient"
parent: hanslin
grand_parent: 貢獻者
tags: [診斷不足, CLAUDE.md規則]
date: 2026-04-14
still_relevant: true
permalink: /contributors/hanslin/013-gradient-override/
---

# background-color 蓋不掉 gradient

## 問題

just-the-docs 的按鈕用 `background-image: linear-gradient(...)` 做紫色漸層。用 `background-color: orange !important` 蓋不掉，因為 `background-image` 的優先級高於 `background-color`。

改了好幾次按鈕顏色，每次都還是紫色。

## 原因

CSS 的 `background-image` 會覆蓋 `background-color`，兩者是不同屬性。Claude 只改了 `background-color`，沒有同時把 `background-image` 設成 `none`。

## 解決方案

覆蓋按鈕顏色時必須同時設定三個屬性。

## 可複用的 CLAUDE.md 規則

```markdown
### CSS 覆蓋
- 覆蓋按鈕或有漸層的元素，MUST 同時設定：
  background-color, background-image: none, box-shadow: none
- 只改 background-color 不夠，gradient 會蓋掉它
```
