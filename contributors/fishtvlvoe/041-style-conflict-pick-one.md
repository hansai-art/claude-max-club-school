---
layout: default
title: "程式碼風格衝突時必須明確選邊站"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/041-style-conflict-pick-one/
tags: [程式碼風格, 一致性, camelCase, 命名規範]
date: 2026-05-18
still_relevant: true
---

# 程式碼風格衝突時必須明確選邊站

## 問題

Claude 在看到 codebase 裡有兩種命名風格混用（例如同時有 `camelCase` 和 `snake_case`）時，沒有選擇其中一種，而是：

- 新加的函式用 camelCase，但新加的 DB 欄位用 snake_case，「因為各有各的慣例」
- 有些地方用 tabs，有些地方用 spaces，「為了兼容原有代碼」
- 同一個 codebase 裡，A 元件用 early-return 風格，B 元件用 nested-if 風格

結果：整個 codebase 的風格逐漸腐爛，新人（或三個月後的自己）看到一頭霧水。

## 原因

Claude 傾向「盡量不破壞現有代碼」，看到兩種風格都存在，會認為兩種都是「允許的」，然後選一個當下方便的繼續用。這種「平均化策略」是 AI 生成代碼的常見病——它讓每個地方都「不那麼錯」，但整體讓 codebase 風格腐爛。

## 解決方案

遇到風格衝突時，強制做一個明確決定：

**步驟 1：查有沒有明確設定**

```bash
cat .editorconfig
cat .prettierrc
cat eslint.config.js | grep rule
```

**步驟 2：沒有設定的話，數哪個佔多數**

```bash
# 計算 camelCase 和 snake_case 的函式數量
grep -c "function [a-z][a-zA-Z]*(" src/ -r || true
grep -c "def [a-z][a-z_]*(" src/ -r || true
```

**步驟 3：無法判斷時，直接問清楚**

> 這個 codebase 同時有 camelCase 和 snake_case，你偏好哪一種？

不允許的做法：
- 「為了兼容性，兩種都保留」
- 「這個檔案用 A，那個檔案用 B」
- 什麼都不說，悄悄混用

## 可複用的 CLAUDE.md 規則

```markdown
## 程式碼風格一致性

- 看到 codebase 有兩種風格衝突時，MUST 先查 .editorconfig/.prettierrc/eslint 設定
- 沒有設定時，數哪種佔多數，跟著多數走
- 無法判斷時直接問：「A 還是 B？」
- 禁止：「為了兼容性兩種都保留」、不聲不響地混用兩種風格
- 一旦決定，同一次任務裡全部統一，不能這個檔案 A 那個檔案 B
```
