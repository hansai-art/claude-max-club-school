---
layout: default
title: "先搜尋現有實作再動手，不要重複造輪子"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/043-reuse-first/
---

# 先搜尋現有實作再動手，不要重複造輪子

## 問題

Claude 開始一個新功能時，直接從頭寫，完全不查 codebase 裡有沒有類似的實作。

常見結果有兩種：
1. 同樣的邏輯在 codebase 裡存在好幾份，未來維護成本倍增
2. Claude 做了一個靜態 UI 外殼，沒接到已有的 API，功能完全不對——但 build 通過，所以它回報「完成」

## 原因

Claude 習慣在空白狀態下「設計」功能，把每次任務都當成全新專案。它不會自動先掃描現有 codebase，除非被明確要求。

在已有一定規模的 codebase（尤其是多人或多週的專案）中，重複造輪子是最常見的浪費。

## 解決方案

在 CLAUDE.md 裡強制「寫任何代碼前先考古」的前置步驟：

1. `grep -r "相關關鍵字" apps/` 找類似 pattern 或函式
2. 確認需要呼叫的 API 是否已存在（procedure/route/hook）
3. 找到後，主動告訴用戶：「這些不用做（已有實作）→ 直接用；只有這些要新寫 → [列清單]」

## 可複用的 CLAUDE.md 規則

```markdown
### reuse-first（先考古再動手，無例外）
- 寫任何代碼前，MUST 先 grep codebase 找類似 pattern 和函式
- 確認 API/procedure/hook 是否已存在，禁止只做 UI 外殼沒接 API
- 開工前主動說明：
  - 「這些已有 → 直接用」
  - 「只有這些要新寫 → [清單]」
- NEVER 從頭寫已經存在的東西
```
