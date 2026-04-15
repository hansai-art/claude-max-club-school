---
layout: default
title: "重複操作必須自動化，不手動重複"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/007-automate-repetitive-tasks/
---

# 重複操作必須自動化，不手動重複

## 問題

需要改 10 個檔案的同一個設定、同步 3 個環境的環境變數、或執行一系列固定步驟，Claude 一個一個手動操作，或者叫用戶自己去手動執行。

這不只效率低，更容易漏掉某個地方，製造不一致。

## 原因

Claude 傾向「最直接的路徑」，直接改 → 下一個 → 繼續改。沒有停下來想「這個操作有沒有規律性？有沒有辦法一次搞定？」

## 解決方案

遇到任何「需要重複改同一件事」的操作，強制問：「這能寫成 script 一次搞定嗎？」

常見可自動化的場景：
- 批次更新多個檔案的同一段文字 → `sed` 或 Python 腳本
- 同步環境變數到多個服務 → `vercel env` + `supabase secrets`
- 重複執行固定指令序列 → Makefile 或 shell script
- 環境變數 `.env` 改了 → 自動同步到 Vercel/Supabase，不叫用戶手動改

## 可複用的 CLAUDE.md 規則

```markdown
## 自動化原則（強制）

任何「需要重複改同一件事」的操作，必須自動化完成，不問用戶：
- 批次修改多個檔案 → 寫 script，一次執行
- 環境變數同步 → 自己用 CLI 同步，不叫用戶手動改
- 重複執行序列 → 包進 Makefile 或 shell function

vercel env / supabase secrets 操作一律用 CLI，不開瀏覽器，不叫用戶手動執行。
```
