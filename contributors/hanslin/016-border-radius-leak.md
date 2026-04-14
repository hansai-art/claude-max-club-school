---
layout: default
title: "圓角在深色模式露出白邊"
parent: hanslin
grand_parent: 貢獻者
tags: [診斷不足, CLAUDE.md規則]
date: 2026-04-14
still_relevant: true
permalink: /contributors/hanslin/016-border-radius-leak/
---

# 圓角在深色模式露出白邊

## 問題

code block 設了 `border-radius: 8px` 做圓角。在深色模式下，外層容器是白色背景，圓角的四個角露出白色，像四個白點。

## 原因

`border-radius` 只裁切元素本身，不會裁切外層容器的背景。如果外層背景色跟內層不同，圓角處會露出外層顏色。

## 解決方案

深色模式不用圓角，或者確保外層容器也是深色。最簡單的方法是全站 `border-radius: 0`。

## 可複用的 CLAUDE.md 規則

```markdown
### 深色模式 CSS
- 有深色底的元素不要用 border-radius，會露出外層白底
- 最安全：全站 * { border-radius: 0 }
```
