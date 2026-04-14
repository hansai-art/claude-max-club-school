---
layout: default
title: 安全規則
parent: 片段庫
nav_order: 2
permalink: /snippets/safety/
---

# 安全規則

防止 Claude 搞壞你的東西。**這裡是 canonical 版本**，其他頁面都連結到這裡。

---

## 檔案操作安全

```markdown
- MUST ls before deleting any directory
- NEVER 執行 sudo、rm -rf /、shutdown、reboot
- NEVER 未經確認 force push
```

---

## 覆蓋保護

來源：[hanslin/005]({{ site.baseurl }}{% link contributors/hanslin/005-no-overwrite-remote.md %})、[hanslin/006]({{ site.baseurl }}{% link contributors/hanslin/006-version-increment.md %})

```markdown
- 修改已發布的內容前，MUST 先從 API 拉取最新版本
- NEVER 用本地舊檔案覆蓋線上內容
- 流程：拉取最新 → 在最新版本上修改 → 推回
- MUST 遞增版本號，NEVER 覆蓋舊版檔案
```

---

## 驗證流程

來源：[hanslin/004]({{ site.baseurl }}{% link contributors/hanslin/004-verify-before-done.md %})、[hanslin/007]({{ site.baseurl }}{% link contributors/hanslin/007-publish-verify-checklist.md %})

```markdown
- CSS/HTML 變更後，MUST fetch 頁面確認關鍵元素存在且可見
- 上傳內容到任何平台後，MUST 用 API 回讀驗證所有必填欄位
- NEVER 直接說「完成」除非你已經驗證結果
```

---

## 資料庫操作

來源：[hanslin/008]({{ site.baseurl }}{% link contributors/hanslin/008-no-manual-sql.md %})

```markdown
- NEVER 叫使用者去 Dashboard 執行 SQL
- NEVER 寫 SQL 檔讓使用者手動執行
- 用 CLI migration 或程式碼處理所有 schema 變更
```

---

## 自動化腳本

來源：[hanslin/003]({{ site.baseurl }}{% link contributors/hanslin/003-automation-debug.md %})

```markdown
- 偵測失敗時 MUST 先記錄實際狀態到 log，再決定是否重試
- Log 要記「期望值」和「實際值」
- NEVER 用同樣的邏輯盲目 retry
```
