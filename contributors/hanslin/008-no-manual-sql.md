---
layout: default
title: "不要叫使用者手動執行 SQL"
parent: hanslin
grand_parent: 貢獻者
tags: [工具誤用, 工作流程]
date: 2026-03-01
still_relevant: true
---

# 不要叫使用者手動執行 SQL

## 問題

Claude 遇到需要修改資料庫 schema 的情況（ALTER TABLE、新增欄位等），會叫使用者去 Supabase Dashboard 執行 SQL，或者寫一個 SQL 檔案叫使用者手動執行。

## 原因

Claude 把「我做不到的事」丟回給使用者，而不是自己找替代方案。在 Lovable 專案中，使用者通常沒有直接操作 Supabase Dashboard 的習慣，這種建議會打斷工作流程。

## 解決方案

所有 DB 操作都由 Claude 自己完成。

## 可複用的 CLAUDE.md 規則

```markdown
### 資料庫操作
- NEVER 叫使用者去 Supabase Dashboard 執行 SQL
- NEVER 寫 SQL 檔讓使用者手動執行
- 用 supabase CLI db push（migration）或程式碼處理所有 schema 變更
- 如果真的做不到，找替代方案（放寬 RLS、用 JSON 欄位、前端 workaround）
```
