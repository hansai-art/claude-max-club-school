---
layout: default
title: "平台操作用 CLI，禁止叫用戶開瀏覽器"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [工具誤用, CLAUDE.md規則]
date: 2026-05-04
still_relevant: true
permalink: /contributors/fishtvlvoe/007-cli-not-browser/
---

# 平台操作用 CLI，禁止叫用戶開瀏覽器

## 問題

Claude 完成一部分工作後說：「現在請你去 Vercel Dashboard 的 Settings → Environment Variables 把這個值加上去」，或「請到 Supabase 控制台執行這個 SQL migration」。

叫用戶開瀏覽器做 Claude 完全可以用 CLI 完成的事，是把本應自動化的工作推回給用戶。

## 原因

Claude 對瀏覽器 GUI 操作的描述比執行 CLI 指令更「安全」（不會搞錯權限），而且不需要考慮指令的正確性。這讓它傾向「描述步驟」而不是「直接執行」。

## 解決方案

**Vercel** 操作一律用 CLI：
- 新增/修改環境變數：`vercel env add` / `vercel env rm`
- 部署：`vercel deploy --prod`
- 讀取環境變數：`vercel env pull`

**Supabase** 操作一律用 CLI：
- 執行 migration：`supabase db push` 或 `psql $DATABASE_URL < migration.sql`
- 管理 secrets：`supabase secrets set`
- 查詢資料庫：`psql $DATABASE_URL -c "..."`

**任何其他需要瀏覽器的操作**：優先查是否有 CLI 或 API 可以完成。只有需要用戶親自授權的事（2FA、付費、手動 Webhook 授權）才例外。

## 可複用的 CLAUDE.md 規則

```markdown
## 平台操作規則
- Vercel 操作一律用 CLI（vercel env / vercel deploy），不叫用戶開瀏覽器
- Supabase 操作一律用 CLI（supabase db / supabase secrets / psql），不叫用戶開瀏覽器
- 禁止「請到 Dashboard 手動做 X」——Claude 有 CLI 就自己做
- 唯一例外：需要用戶親自授權（2FA、付費操作、手動 Webhook 授權）
```
