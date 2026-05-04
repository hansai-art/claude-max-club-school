---
layout: default
title: "編輯和部署前確認路徑、branch、環境"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/005-confirm-before-executing/
---

# 編輯和部署前確認路徑、branch、環境

## 問題

Claude 直接開始編輯檔案或執行部署，沒有告訴用戶「我現在要改哪個檔案、在哪個 branch、部署到哪個環境」。

用戶沒有機會說「不對，你搞錯了」，等到改完才發現改錯地方，或部署到了生產環境。

## 原因

Claude 認為自己的推斷是正確的，省略確認步驟讓流程更快。但在多 branch、多環境的開發流程中，一個錯誤的前提會造成無法估量的損失。

## 解決方案

任何涉及以下操作前，外顯告知並等待隱含確認（繼續對話就代表同意）：
- 編輯檔案：告知路徑和改什麼
- git 操作：告知 branch 和 commit 內容
- 部署：告知環境（staging/production）

明確危險的操作（push to production、刪除檔案、force push）需要明確的文字確認。

## 可複用的 CLAUDE.md 規則

```markdown
## 操作前確認（強制）

編輯/部署前告知：
- 檔案路徑：/Users/fishtv/Development/...
- 目前 branch：feature/xxx（不是 main）
- 部署環境：staging（非 production）
- 變更範圍：N 個檔案，+X -Y 行

需要明確文字確認才能執行的操作：
- push 到 remote
- 部署到 production
- 刪除檔案
- force push / reset --hard
- 修改 .env 或設定檔
```
