---
layout: default
title: "UI 任務 commit 前必須截圖視覺驗證"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [前端開發, 工作流程]
date: 2026-05-04
still_relevant: true
permalink: /contributors/fishtvlvoe/011-screenshot-before-ui-commit/
---

# UI 任務 commit 前必須截圖視覺驗證

## 問題

Claude 完成 HTML/CSS/React 元件修改，跑 `grep` 確認關鍵字存在，就 commit 並回報「完成」。

但實際在瀏覽器看：tab 切換邏輯壞了、元件顯示錯誤的內容、CSS 沒有生效。Grep 通過不代表視覺正確。

真實案例：同一個 HTML 頁面的 tab 邏輯踩了兩次同樣的坑——`grep` 顯示 tab 內容都在，但截圖才發現兩個 tab 都顯示同一組 onboarding 內容，execution tab 根本沒切換。

## 原因

Claude 用「字面驗證」代替「行為驗證」：
- HTML 結構正確 ≠ 瀏覽器渲染正確
- CSS 語法正確 ≠ 視覺效果正確
- JavaScript 邏輯正確 ≠ UI 交互正確

跑 `grep` 只能驗證程式碼有沒有寫進去，無法驗證它在瀏覽器的實際行為。

## 解決方案

UI 任務（HTML 原型、React 元件、CSS 改動）commit 前，MUST 用 playwright 或 chrome MCP 截圖每個畫面和狀態：

1. 對每個畫面/狀態截圖存到 `/tmp/`
2. Read 截圖確認渲染正確
3. 有問題就退回修改，不能「Agent 回報完成 + grep 通過」就 commit

這是「客觀證據」對「主觀回報」的差別——截圖才是客觀證據。

## 可複用的 CLAUDE.md 規則

```markdown
## UI 任務驗證規則
- UI 任務（HTML/CSS/React）commit 前：MUST 用 playwright 截圖每個畫面和狀態
- 步驟：截圖存 /tmp/ → Read 確認渲染對 → 錯誤就退回改
- 禁止「grep 字串存在」就 commit——字面驗證 ≠ 行為驗證
- 派工給子代理做 UI 時，prompt 必須要求：「完成後截圖存到 /tmp/ 並列出路徑，不說完成，說截圖在 X 請主對話驗證」
```
