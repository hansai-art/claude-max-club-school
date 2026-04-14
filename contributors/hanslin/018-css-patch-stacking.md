---
layout: default
title: "CSS 疊 patch 不診斷根因"
parent: hanslin
grand_parent: 貢獻者
tags: [盲目重試, 工作流程]
date: 2026-04-14
still_relevant: true
permalink: /contributors/hanslin/018-css-patch-stacking/
---

# CSS 疊 patch 不診斷根因

## 問題

CSS 出問題時，Claude 的反應是「加更多 CSS 規則」。按鈕顏色不對？加一條 `!important`。還不對？再加一條更具體的 selector。還不對？再加。

結果 CSS 從 80 行膨脹到 240 行，問題還是沒解決。最後整份重寫反而只要 120 行。

## 原因

跟程式碼 debug 一樣，Claude 傾向「疊修」而不是「重診斷」。CSS 的 cascade 機制讓疊修特別危險，因為優先級規則很複雜。

## 解決方案

CSS 改兩次還沒修好，STOP，重新診斷。先用 curl 抓 theme CSS，列出所有影響目標元素的規則和優先級，找到根因後一次改對。

## 可複用的 CLAUDE.md 規則

```markdown
### CSS Debug
- CSS 改兩次沒修好，STOP 重新診斷
- 先 curl 抓 theme CSS，列出影響目標元素的所有規則
- 確認 selector 優先級夠高才動手
- 寧可整份重寫也不要繼續疊 patch
```
