---
layout: default
title: "先診斷再動手"
parent: hanslin
grand_parent: 貢獻者
permalink: /contributors/hanslin/002-diagnose-first/
---

# 先診斷再動手：不要讓 Claude 猜答案

## 問題

Claude Code 遇到 bug 或 UI 問題時，傾向直接「猜」答案並開始改 code。如果第一次沒猜對，它會在錯的方向上繼續疊 patch，越改越糟。

真實案例：修改網站首頁文章卡片的 CSS 樣式，Claude 反覆嘗試了 4-5 輪不同的 CSS，每一輪都是猜測加盲改。結果浪費大量 token，問題越改越糟。

在我的使用數據中，73 次「wrong approach」是最大的 token 浪費來源。

## 原因

Claude 很「急著幫忙」。它收到問題描述後，會立刻根據經驗猜測原因並開始修改，而不是先收集資料確認根因。這在簡單問題上有效，但在複雜問題（特別是 CSS、資料庫 schema、API 行為）上會翻車。

## 解決方案

強制 Claude 遵循「診斷 → 確認 → 修改」的流程，並且明確禁止在同一個方向上重試。

## 可複用的 CLAUDE.md 規則

```markdown
### Diagnose Before Fixing
- MUST 先列 2-3 個可能原因，讀 code 確認根本原因，才動手
- 修法不 work，重新診斷，NEVER 疊 patch

### CSS/UI 修改
- 修改 CSS 前，先 fetch 頁面 HTML，用精確的 selector 找出造成問題的具體 CSS rule
- 列出根因和修改方案，確認後才執行
- 如果第一輪沒修好，STOP，重新診斷，不要在錯的方向上疊 patch

### 通用問題排查
- 遇到問題先跑診斷指令確認根因，不要猜測
- 不要重複已經試過但失敗的建議
- 失敗後不盲目重試，先讀錯誤訊息診斷原因
```
