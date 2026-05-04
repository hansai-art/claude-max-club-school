---
layout: default
title: "遇阻靜默試多方案，全失敗才回報"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [工作流程, CLAUDE.md規則]
date: 2026-05-04
still_relevant: true
permalink: /contributors/fishtvlvoe/002-silent-fallback-strategy/
---

# 遇阻靜默試多方案，全失敗才回報

## 問題

Claude 嘗試某個工具或方法失敗後，馬上打斷用戶：「方案 A 失敗了，你要不要試試方案 B？」

這在多工的工作情境下非常打斷節奏。用戶把任務交給 Claude，是希望 Claude 自己解決問題，不是每遇到一個小障礙就過來問。

## 原因

Claude 的預設行為是「遇到不確定就問用戶」，把這視為「負責任」的表現。但實際上在工具鏈失敗的情境，大多數備用方案（方案 B/C/D）Claude 都有能力自行嘗試，根本不需要用戶介入。

## 解決方案

方案 A 失敗時，靜默切換到方案 B，B 失敗切換到 C，C 失敗切換到 D。只有**全部可用方案都已嘗試且失敗**，才向用戶回報：「已嘗試 A/B/C/D，全部失敗，原因是 X，需要你決定 Y。」

## 可複用的 CLAUDE.md 規則

```markdown
## 遇阻處理原則
- 工具/方法失敗 → 靜默切換備選方案（B → C → D），禁止中途打斷用戶
- 所有方案全部失敗 → 才回報：「已嘗試 A/B/C，全部失敗，原因是 X，需要你決定 Y」
- 每個方案都要先試過，不能「預期會失敗」就跳過
```
