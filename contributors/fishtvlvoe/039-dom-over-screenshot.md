---
layout: default
title: "分析 UI 結構要讀 DOM，不要截圖"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/039-dom-over-screenshot/
tags: [UI, DOM, token效率, 截圖, 分析]
date: 2026-05-18
still_relevant: true
---

# 分析 UI 結構要讀 DOM，不要截圖

## 問題

Claude 在分析 UI 結構（排版問題、CSS 值、元件層級）時，直接用 Playwright 或 Chrome MCP 截圖，再「看圖說話」推斷 class name 和 CSS 數值。

這個方式有兩個根本問題：

1. **Token 浪費**：一張截圖消耗約 1,500 tokens，但得到的是「大概看起來是 padding 16px」這種模糊推測
2. **精準度低**：截圖無法看到 computed style、class hierarchy、實際 hex color、z-index 等關鍵資訊

真實案例：Claude 截圖後猜「background 是 #333 左右的深灰」，實際是 `oklch(0.278 0.033 256.84)`，完全不是一回事。

## 原因

截圖是給人看的介面。AI 看截圖需要先把視覺資訊解碼回文字，再用文字推理，等於做了兩次轉換。

但 AI 的原生介面是文字。直接讀 DOM 和 CSS 能拿到精確數值，消耗的 token 反而更少。

## 解決方案

分析 UI 結構時，用 Browser MCP 的文字工具直接讀 DOM：

```javascript
// 取得元素的 computed style
await page.evaluate(() => {
  const el = document.querySelector('.card-header');
  const style = window.getComputedStyle(el);
  return {
    padding: style.padding,
    backgroundColor: style.backgroundColor,
    fontSize: style.fontSize,
    zIndex: style.zIndex,
    display: style.display,
  };
});
```

```javascript
// 取得頁面結構
const html = await page.innerHTML('main');
// 或只取文字
const text = await page.innerText('nav');
```

截圖只保留給**最終視覺驗證**（確認渲染結果是否符合設計稿）。分析結構和偵錯 CSS 的過程，一律讀代碼。

## 可複用的 CLAUDE.md 規則

```markdown
## UI 分析工具選擇

- 分析 UI 結構（class、padding、color、z-index）→ 用 Browser MCP 讀 DOM/computed style
- 截圖只用於最終視覺驗證（確認渲染結果符合設計稿）
- 禁止用截圖來「推斷」CSS 數值，截圖無法精確讀出 hex color、computed px、class hierarchy
- 給人看的是圖形介面，給 AI 看的是 0 與 1 的文字介面
```
