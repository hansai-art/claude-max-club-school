---
layout: default
title: "任何需要重複操作的事，必須自動化完成"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [工作流程, CLAUDE.md規則]
date: 2026-05-04
still_relevant: true
permalink: /contributors/fishtvlvoe/006-automate-dont-ask/
---

# 任何需要重複操作的事，必須自動化完成

## 問題

改了 A 檔案，Claude 告訴用戶：「現在你需要去 B 設定檔也做同樣的修改」。或是同步 `.env` 到多個平台時，Claude 修改了本地 `.env`，然後說「你需要把這個同步到 Vercel 和 Supabase」。

把重複的、可腳本化的操作推給用戶，是最常見的「名義上完成、實際上沒完成」的情形。

## 原因

Claude 傾向「告知」而不是「執行」。這部分是因為 Claude 擔心越權（「用戶可能不想讓我動那個檔案」），但在絕大多數開發任務裡，這種謹慎是多餘的。用戶請 Claude 完成一個任務，就是要 Claude 把整件事做完，不是告知要做什麼。

## 解決方案

任何「需要重複改同一件事」的操作，Claude 必須自動化完成：

- 多個檔案需要同步修改 → 寫腳本或一次改完
- `.env` 改了需要同步到遠端平台 → 自己跑 `vercel env add` / `supabase secrets set`
- 改了配置需要同步更新相依的地方 → 自己找到並改完

只有用戶需要「親自判斷」或「提供外部資訊」的事才能停下來等。

## 可複用的 CLAUDE.md 規則

```markdown
## 自動化原則
- 任何「需要重複改同一件事」的操作：MUST 自動化完成，不問用戶
- 禁止「你現在需要去 X 做 Y」——那是把用戶當執行工具
- 唯一可以等待用戶的情況：需要用戶的業務判斷，或需要用戶提供外部資訊
```
