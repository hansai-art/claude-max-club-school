---
layout: default
title: "Postgres schema 演進用 ALTER TABLE，CREATE TABLE IF NOT EXISTS 是 no-op"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [資料庫, 診斷不足]
date: 2026-05-04
still_relevant: true
permalink: /contributors/fishtvlvoe/034-postgres-alter-not-create/
---

# Postgres schema 演進用 ALTER TABLE，CREATE TABLE IF NOT EXISTS 是 no-op

## 問題

在 production 資料庫需要新增欄位，Claude 寫了一個 migration：

```sql
CREATE TABLE IF NOT EXISTS my_table (
  id SERIAL PRIMARY KEY,
  existing_col TEXT,
  new_col VARCHAR(255)  -- 新加的欄位
);
```

Migration 執行成功，沒有錯誤。但 `new_col` 欄位根本沒有被加進去。

## 原因

`CREATE TABLE IF NOT EXISTS` 的行為是：
- 表**不存在** → 建立整張表（含所有欄位）
- 表**已存在** → **完全不做任何事**（no-op）

Production 的 `my_table` 早就存在了，所以整個 CREATE TABLE 語句被靜默跳過。Migration 「成功執行」但什麼都沒改。

Claude 看 migration 檔案以為欄位應該在，實際去查才發現不在。然後開始以為是其他問題，花了很多時間排查。

## 解決方案

Schema 演進（修改已存在的表）必須用 `ALTER TABLE`：

```sql
-- 新增欄位
ALTER TABLE my_table ADD COLUMN IF NOT EXISTS new_col VARCHAR(255);

-- 擴展 CHECK 約束（需要先 DROP 再 ADD）
DO $$
BEGIN
  ALTER TABLE my_table DROP CONSTRAINT IF EXISTS my_check_constraint;
  ALTER TABLE my_table ADD CONSTRAINT my_check_constraint
    CHECK (status IN ('pending', 'active', 'cancelled'));
END $$;
```

**Debug 時先查 production 真實 schema**，不要憑 migration 檔案推論：

```bash
psql $DATABASE_URL -c "\d my_table"
```

## 可複用的 CLAUDE.md 規則

```markdown
## Postgres schema 演進
- 修改已存在的表：MUST 用 ALTER TABLE ADD COLUMN IF NOT EXISTS
- 禁止用 CREATE TABLE IF NOT EXISTS 新增欄位——在已存在的表上是 no-op，靜默什麼都不做
- DEBUG 前先確認 production 真實 schema：psql $DATABASE_URL -c "\d <table>"
- 不要憑 migration 檔案推論 schema 狀態——CREATE TABLE IF NOT EXISTS 可能從來沒生效過
```
