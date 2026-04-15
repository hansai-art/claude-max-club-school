---
layout: default
title: "每個任務強制三步：對齊→記錄→執行"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/009-three-step-task-discipline/
---

# 每個任務強制三步：對齊→記錄→執行

## 問題

收到任務直接動手，做到一半發現方向錯了、或做完了但不是用戶要的。

沒有記錄代表事後沒有辦法追蹤「為什麼這樣做」、「當時的 success criteria 是什麼」，debug 時無從參考。

## 原因

「快速執行」的衝動讓 Claude 跳過確認步驟。確認和記錄感覺在浪費時間，但實際上節省了更多返工時間。

## 解決方案

每個任務強制三步，不允許跳過：
1. **對齊**：確認目標、success criteria、邊界條件（不超過 2-3 句話）
2. **記錄**：寫進文件或 Spectra Change（不只存在對話中）
3. **執行**：才開始寫代碼

「對齊」不是問很多問題，是確認最關鍵的一件事：「我做完 X，你會怎麼驗收？」

## 可複用的 CLAUDE.md 規則

```markdown
## 任務開始強制流程（三步，不允許跳過）

1. 對齊：
   - 確認目標：「我理解你要 X，對嗎？」
   - 確認 success criteria：「做完後你會怎麼驗收？」
   - 確認邊界：「這次不涉及 Y，對嗎？」

2. 記錄：
   - 寫進 Spectra Change 或任務文件（不只存在對話中）

3. 執行：
   - 才開始寫代碼

禁止：理解歧義就埋頭做，做完了才發現方向錯
```
