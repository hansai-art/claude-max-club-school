---
layout: default
title: "Supabase 操作一律用 CLI，不開瀏覽器"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [自動化原則, CLAUDE.md規則]
date: 2026-04-01
still_relevant: true
permalink: /contributors/fishtvlvoe/016-supabase-cli-only/
---

# Supabase 操作一律用 CLI，不開瀏覽器

## 問題

Claude 在需要執行 Supabase migration 或管理 secrets 時，會叫用戶「去 Supabase Dashboard 貼這段 SQL」或「打開瀏覽器到 Settings > API 複製 key」。這打斷了工作流程，而且完全可以用 CLI 自動完成。

## 原因

Claude 對 Supabase CLI 的使用習慣不夠積極，傾向於提供「用戶手動操作」的步驟，因為這樣更直觀易懂。但對於開發者工作流來說，這是低效的做法。

## 解決方案

**Migration 操作：** 使用 `supabase db` + DB URL 直接執行，不叫用戶貼 SQL：

```bash
# 執行 migration
supabase db push --db-url "postgresql://..."

# 或用 psql 直接執行
psql "$DATABASE_URL" -f migration.sql
```

**Secrets 操作：** 使用 `supabase secrets set` 管理環境變數：

```bash
supabase secrets set MY_KEY=value --project-ref <ref>
```

**查看資料：** 使用 `supabase db` 或 `psql` 直接查詢，不需要打開 Dashboard。

規則：所有可以用 CLI 完成的 Supabase 操作，Claude 應自行執行完畢，不需要用戶介入瀏覽器。

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- Supabase 操作一律用 CLI（supabase db / supabase secrets），不開瀏覽器、不叫用戶手動操作。
  Migration 直接用 CLI + DB URL 執行，secrets 用 supabase secrets set。
```
