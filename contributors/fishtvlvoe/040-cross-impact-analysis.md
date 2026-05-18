---
layout: default
title: "寫代碼前先做 cross-impact 分析（A 壞 B 預檢）"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/040-cross-impact-analysis/
tags: [預防, 影響分析, 重構, API, 測試]
date: 2026-05-18
still_relevant: true
---

# 寫代碼前先做 cross-impact 分析（A 壞 B 預檢）

## 問題

Claude 修改 A 功能，不知道 B 功能依賴 A，結果改完 A、B 就壞了。

常見的模式：

- 修改 API endpoint 的回傳格式，前端 10 個地方都打這個 API，全部炸掉
- 重命名 DB 欄位，有 5 個 query 用到舊欄位名，全部 runtime error
- 修改共用 utility function 的參數簽名，有 8 個 caller 沒更新，型別錯誤

更隱蔽的情況：後端 service method 的 caller 只有一個，但前端打的是另一個 REST endpoint，改了 service method 以為修好了，其實前端打的那個 endpoint 用的是另一個 SQL，根本沒影響到。

## 原因

Claude 專注在被要求修改的那個地方，沒有習慣性地往外追蹤「誰用了我要改的東西」。光搜 service method 的 caller 不夠——前端打的 REST URL 和後端 service method 之間可能根本沒有直接對應。

## 解決方案

改任何 API/函式/DB 欄位前，先做 cross-impact 分析：

```bash
# 找所有打這個 API endpoint 的前端代碼
grep -r "fetch.*\/api\/orders" src/ --include="*.ts" --include="*.tsx"
grep -r "\/orders\/" src/components/ src/pages/

# 找所有呼叫這個函式的地方
grep -rn "getOrderItems\|get_order_items" src/ --include="*.ts"

# 找所有用到這個 DB 欄位的 query
grep -rn "supplier_id" src/ --include="*.ts"
```

把找到的依賴分類：

| 等級 | 意義 | 動作 |
|------|------|------|
| ✅ 無影響 | 沒有 caller 使用被改的介面 | 直接改 |
| ⚠️ 需注意 | 有 caller 但介面沒改變，只是行為微調 | 補測試後改 |
| 🔴 高風險 | 有多個 caller、介面會改變 | 停下來，先更新所有 caller |

修改 REST API 行為前的特殊步驟：先從前端往後 trace（grep fetch URL → 找實際被打的 endpoint → 才改對應 handler），不能只看 service method 的 caller。

## 可複用的 CLAUDE.md 規則

```markdown
## Cross-impact 分析（改 A 不壞 B）

- 修改任何 API endpoint、函式簽名、DB 欄位前，MUST 先 grep 所有 caller 和 consumer
- 分析結果分三級：✅ 無影響 / ⚠️ 需注意 / 🔴 高風險
- 🔴 高風險 → STOP，先列出完整影響範圍再動手
- 修改 REST API 行為前 MUST 從前端往後 trace：grep fetch URL → 找前端實際打的 endpoint → 才改對應 handler
- 光看 service method 的 caller 不夠，前端打的 endpoint 可能用完全獨立的 SQL
```
