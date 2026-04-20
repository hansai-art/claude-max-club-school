---
layout: default
title: "覆蓋漸層元素必須同時清除 background-image 和 box-shadow"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [CSS, CLAUDE.md規則]
date: 2026-04-01
still_relevant: true
permalink: /contributors/fishtvlvoe/020-gradient-override/
---

# 覆蓋漸層元素必須同時清除 background-image 和 box-shadow

## 問題

要覆蓋一個有漸層背景的按鈕或元素，只改 `background-color` 沒有效果。漸層仍然顯示，顏色蓋不上去。

## 原因

CSS 的 `background` 是多層屬性的合集：

- `background-color`：純色背景（最底層）
- `background-image`：漸層（`linear-gradient` 等）覆蓋在 `background-color` 之上
- `box-shadow`：按鈕常用 `box-shadow` 模擬立體感，也可能帶有顏色

當你只設定 `background-color` 時，`background-image`（漸層）仍然存在，並且渲染在純色之上，所以漸層會蓋掉你設定的顏色，看起來像是「改了但沒效果」。

## 解決方案

覆蓋漸層元素時，**MUST 同時設定三個屬性**：

```css
.target-button {
  background-color: #your-color !important;
  background-image: none !important;
  box-shadow: none !important;
}
```

或用 shorthand 一次清除：

```css
.target-button {
  background: #your-color !important;
  box-shadow: none !important;
}
```

`background` shorthand 會自動重置 `background-image` 為 `none`。

**排查步驟：** 如果改了顏色但看起來沒效果，在 DevTools > Computed styles 搜尋 `background`，看有沒有 `background-image: linear-gradient(...)` 還在作用。

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- 覆蓋有漸層的按鈕或元素，MUST 同時設定：
  background-color: X + background-image: none + box-shadow: none
  只改 background-color 不夠，漸層會蓋掉純色。
```
