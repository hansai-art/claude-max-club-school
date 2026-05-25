---
layout: default
title: "擴展點名稱必須查文件確認，不猜檔名"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [平台整合, 診斷不足]
date: 2026-04-01
still_relevant: true
permalink: /contributors/fishtvlvoe/023-verify-extension-names/
---

# 擴展點名稱必須查文件確認，不猜檔名

## 問題

Claude 在使用框架的擴展點時（WordPress hook 名稱、Jekyll include 名稱、React context slot 等），有時會「猜」名稱，用看起來合理的命名，結果用了不存在的 hook 或 include，導致功能靜默失敗——代碼沒有錯誤，但也什麼事都沒發生。

例如：
- WordPress：用了 `woocommerce_after_order_table` 而實際 hook 是 `woocommerce_order_details_after_order_table`
- Jekyll：用了 `{% include sidebar.html %}` 但實際檔案是 `_includes/sidebar.liquid`

## 原因

Claude 對常見框架有一定知識，但 hook/include/slot 名稱很容易有細微差異，而且不同版本間可能有變化。猜測看起來「合理」的名稱，但正確性無法保證。

## 解決方案

使用任何擴展點（include、hook、slot、event name）之前，MUST 先確認正確名稱：

**WordPress：**
```bash
# 在 WooCommerce 原始碼中搜尋 hook 名稱
grep -r "do_action\|apply_filters" vendor/woocommerce/ | grep "order_details"
```

**Jekyll：**
```bash
# 確認 _includes 下的實際檔名
ls _includes/
```

**一般原則：**
1. 優先查官方文件（搜尋確切的 hook/event 名稱）
2. 其次在原始碼中 grep 確認
3. 最後才考慮「命名慣例推斷」——但仍需測試驗證

靜默失敗（沒有 error 但功能不動）通常是擴展點名稱錯誤的症狀，這時第一步就是驗證名稱。

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- 任何擴展點（include/hook/slot/event）用前 MUST 先查文件確認正確名稱，不猜檔名。
  靜默失敗（無 error 但功能不動）→ 優先懷疑擴展點名稱錯誤。
```
