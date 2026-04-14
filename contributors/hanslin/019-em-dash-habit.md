---
layout: default
title: "明確禁止的符號還是一直用"
parent: hanslin
grand_parent: 貢獻者
tags: [盲目重試, CLAUDE.md規則]
date: 2026-04-14
still_relevant: true
permalink: /contributors/hanslin/019-em-dash-habit/
---

# 明確禁止的符號還是一直用

## 問題

CLAUDE.md 明確寫了「NEVER 用 em dash（—），改用冒號（：）」。但 Claude 在整個專案裡用了 28 處 em dash，直到使用者發現才全部替換。

## 原因

Claude 把 CLAUDE.md 的規則當「建議」而不是「硬規則」。在寫文件時自動使用 em dash 因為它是英文寫作的慣例。

## 解決方案

```markdown
### 硬規則
- CLAUDE.md 裡標記 NEVER 的事項是絕對禁止，不是建議
- 寫完任何文字內容後，grep 一次禁止的符號和格式
```
