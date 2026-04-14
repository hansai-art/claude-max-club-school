---
layout: default
title: "修完要自己驗證才能說完成"
parent: hanslin
grand_parent: 貢獻者
tags: [盲目重試, CLAUDE.md規則]
date: 2026-04-02
still_relevant: true
permalink: /contributors/hanslin/004-verify-before-done/
---

# 修完要自己驗證才能說完成

## 問題

Claude 修改 CSS、JS、API 設定後，會直接回報「完成了」，但其實根本沒有驗證結果是否正確。

真實案例：修改搜尋彈窗的 CSS，Claude 回報「完成」，但實際上搜尋框內容完全沒顯示，只有一個白色空框和一個 X 按鈕。

## 原因

Claude 傾向樂觀回報。它知道自己執行了正確的指令（例如成功 push 了 CSS），就假設結果一定正確。但 CSS 的效果取決於整個頁面的 DOM 結構和其他樣式的交互作用，光看自己寫的 CSS 是判斷不了的。

## 解決方案

強制 Claude 在回報「完成」之前先驗證。

## 可複用的 CLAUDE.md 規則

```markdown
### 驗證
- CSS/HTML 變更後，MUST fetch 頁面確認關鍵元素存在且可見
- JS 注入後，確認 script 有被載入
- 如果無法直接驗證，告訴使用者「已修改，但我無法完全驗證，請你確認」
- NEVER 直接說「完成」除非你已經驗證結果
```
