---
layout: default
title: "UI 按鈕圖示用 SVG，禁止 Emoji"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [前端開發, CLAUDE.md規則]
date: 2026-05-04
still_relevant: true
permalink: /contributors/fishtvlvoe/003-svg-not-emoji/
---

# UI 按鈕圖示用 SVG，禁止 Emoji

## 問題

Claude 在設計 UI 元件時，習慣用 Emoji 當作圖示：「✅ 完成」、「❌ 刪除」、「📦 訂單」、「⚠️ 警告」。

這在生產環境 UI 看起來非常不專業，而且 Emoji 在不同作業系統/字型下渲染不一致（iOS 的 ✅ 和 Windows 的 ✅ 顏色、大小、風格都不一樣）。

## 原因

Emoji 是 Unicode 字元，可以直接插入文字，Claude 不需要額外的工具就能「放圖示」。相比之下，SVG icon 需要引入 icon library 或貼 SVG 原始碼，Claude 覺得麻煩。

## 解決方案

UI 中的所有圖示一律使用 SVG icon，優先採用 Heroicons 或 Lucide React 這類有 npm package 的 icon library。不需要安裝時，貼入 inline SVG 也可以，但絕對不用 Emoji 字元。

## 可複用的 CLAUDE.md 規則

```markdown
## UI 圖示規則
- UI 按鈕、標籤、狀態、圖示：一律用 SVG icon（Heroicons/Lucide React）
- 禁止使用 Emoji 字元作為 UI 圖示
- 需要 inline 時，直接貼 <svg>...</svg>，不用 Emoji
- 文字內容（如說明文件、commit message）不受此限制
```
