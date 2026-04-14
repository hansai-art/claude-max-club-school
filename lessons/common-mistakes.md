---
layout: default
title: 常見錯誤
parent: 經驗分類
nav_order: 1
permalink: /lessons/common-mistakes/
---

# 常見錯誤

Claude Code 最常犯的錯。按「問題類型」分類，連結到貢獻者的原文。

---

## 工具誤用

| 問題 | 貢獻者 | 驗證人數 |
|:-----|:-------|:--------|
| [用 Write 覆蓋整檔而不是 Edit 改 diff]({{ site.baseurl }}{% link contributors/hanslin/001-edit-not-write.md %}) | hanslin | 1 |
| [不要叫使用者手動執行 SQL]({{ site.baseurl }}{% link contributors/hanslin/008-no-manual-sql.md %}) | hanslin | 1 |

## 盲目重試

| 問題 | 貢獻者 | 驗證人數 |
|:-----|:-------|:--------|
| [遇到 bug 直接猜答案不先診斷]({{ site.baseurl }}{% link contributors/hanslin/002-diagnose-first.md %}) | hanslin | 1 |
| [自動化腳本失敗只會盲目重試]({{ site.baseurl }}{% link contributors/hanslin/003-automation-debug.md %}) | hanslin | 1 |
| [修完直接說完成不驗證]({{ site.baseurl }}{% link contributors/hanslin/004-verify-before-done.md %}) | hanslin | 1 |
| [發布後不 API 回讀確認]({{ site.baseurl }}{% link contributors/hanslin/007-publish-verify-checklist.md %}) | hanslin | 1 |

## 覆蓋風險

| 問題 | 貢獻者 | 驗證人數 |
|:-----|:-------|:--------|
| [用本地舊檔覆蓋遠端內容]({{ site.baseurl }}{% link contributors/hanslin/005-no-overwrite-remote.md %}) | hanslin | 1 |
| [覆蓋舊版檔案不遞增版本號]({{ site.baseurl }}{% link contributors/hanslin/006-version-increment.md %}) | hanslin | 1 |

## token 浪費

| 問題 | 貢獻者 | 驗證人數 |
|:-----|:-------|:--------|
| [讀整個檔案而不是只讀需要的部分]({{ site.baseurl }}{% link contributors/hanslin/010-read-only-what-you-need.md %}) | hanslin | 1 |
| [能同時做的事分成多輪做]({{ site.baseurl }}{% link contributors/hanslin/009-parallel-tool-calls.md %}) | hanslin | 1 |

---

**驗證人數** = 多少個貢獻者獨立發現同樣的問題。你也遇過？[貢獻你的經驗]({{ site.baseurl }}{% link pages/getting-started.md %})，驗證人數 +1。
