---
layout: default
title: "Postgres CREATE TABLE IF NOT EXISTS 不會升級既有的表"
parent: fishtvlvoe
grand_parent: 貢獻者
date: 2026-05-11
still_relevant: true
permalink: /contributors/fishtvlvoe/010-postgres-create-table-no-upgrade/
---

# Postgres `CREATE TABLE IF NOT EXISTS` 不會升級既有的表

## 問題

Claude 在 migration 檔案裡用 `CREATE TABLE IF NOT EXISTS` 新增欄位，執行成功，沒有任何 error，但 production 資料庫的表依然缺少那些欄位。之後呼叫 API 出現「column XXX does not exist」錯誤。

真實案例：修改 `processed_emails` 表，想新增 `status` 和 `error_message` 欄位。Migration 檔案用 `CREATE TABLE IF NOT EXISTS processed_emails (id, status, error_message, ...)` 重新定義整張表，執行結果顯示「CREATE TABLE」但欄位沒有出現，直到 `\d processed_emails` 才發現表根本沒有改。

## 原因

`CREATE TABLE IF NOT EXISTS` 的語義是「如果表不存在，就建立」。**如果表已經存在，整個 CREATE TABLE 語句就是 no-op**，不會新增欄位、不會改欄位型別、不會修改約束。

這個行為完全符合 SQL 標準，但很容易誤解。Migration 檔案執行成功（沒有 error），給人一種「改動已套用」的錯誤印象。

## 解決方案

Schema 演進必須用 `ALTER TABLE`：

```sql
-- 新增欄位（如果不存在）
ALTER TABLE processed_emails
  ADD COLUMN IF NOT EXISTS status TEXT NOT NULL DEFAULT 'pending',
  ADD COLUMN IF NOT EXISTS error_message TEXT;

-- 修改 CHECK 約束
DO $$
BEGIN
  ALTER TABLE processed_emails DROP CONSTRAINT IF EXISTS check_status;
  ALTER TABLE processed_emails ADD CONSTRAINT check_status
    CHECK (status IN ('pending', 'processed', 'failed', 'skipped'));
END $$;
```

**Debug 前先查 production 真實 schema**，不要憑 migration 檔案推論：

```bash
psql $DATABASE_URL -c "\d processed_emails"
```

## 可複用的 CLAUDE.md 規則

```markdown
### Postgres Schema 演進
- CREATE TABLE IF NOT EXISTS 不會升級既有表——對已存在的表是 no-op
- Schema 演進 MUST 用 ALTER TABLE ... ADD COLUMN IF NOT EXISTS
- CHECK 約束擴展：DO $$ DROP CONSTRAINT ... ADD CONSTRAINT $$
- Debug 假設前先查 production 真實 schema（psql -c "\d <table>"）
- 不要憑 migration 檔案推論 production 狀態——CREATE TABLE 看起來成功可能是 no-op
```
