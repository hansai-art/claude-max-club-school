---
layout: default
title: "每次更新都要遞增版本號"
parent: hanslin
grand_parent: 貢獻者
tags: [覆蓋風險, CLAUDE.md規則]
date: 2026-03-10
still_relevant: true
---

# 每次更新都要遞增版本號

## 問題

Claude 產出影片、PDF、或其他檔案時，會直接覆蓋同名的舊檔案，導致歷史版本消失。

## 原因

Claude 預設行為是「更新 = 覆蓋同一個檔案」，它不會自動加版本號。

## 解決方案

```markdown
### 版本
- MUST 遞增版本號。NEVER 覆蓋舊版檔案。
- 例如：iPAS_初級_v5.mp4，下次就是 _v6.mp4
```
