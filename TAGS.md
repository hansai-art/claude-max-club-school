---
layout: default
title: 標籤分類
nav_order: 8
---

# 標籤分類
{: .fs-8 }

所有經驗文章的 `tags` 必須從以下清單中選擇。
{: .fs-5 .fw-300 }

請勿自創標籤。如果你覺得需要新標籤，[開 Issue 建議](https://github.com/hansai-art/claude-max-club-school/issues/new/choose)。

---

## 問題類型

| 標籤 | 說明 | 範例 |
|:-----|:-----|:-----|
| `工具誤用` | Claude 用錯工具或用低效的方式操作 | 用 Write 覆蓋整檔而非 Edit |
| `盲目重試` | 失敗後不診斷就重複同樣操作 | CSS 盲改、retry 迴圈 |
| `覆蓋風險` | Claude 覆蓋了不該覆蓋的內容 | 本地舊檔蓋掉遠端新版 |
| `診斷不足` | 沒有先確認根因就動手修 | 猜答案、疊 patch |
| `token浪費` | 不必要的 token 消耗 | 重讀檔案、冗長回應 |
| `安全疏忽` | 有潛在破壞性的操作 | 未確認 force push、rm -rf |

## 工作場景

| 標籤 | 說明 |
|:-----|:-----|
| `前端開發` | React、Vue、CSS、HTML |
| `後端開發` | API、資料庫、伺服器 |
| `WordPress` | WP 文章、主題、外掛 |
| `自動化` | 排程腳本、CI/CD、部署 |
| `內容創作` | 文章撰寫、SEO、翻譯 |
| `DevOps` | Docker、部署、監控 |
| `資料庫` | SQL、Supabase、PostgreSQL |

## 解決方式

| 標籤 | 說明 |
|:-----|:-----|
| `CLAUDE.md規則` | 透過 CLAUDE.md 規則解決 |
| `提示技巧` | 透過改變提示方式解決 |
| `工作流程` | 透過改變工作流程解決 |
| `hooks` | 透過 Claude Code hooks 解決 |
