---
layout: default
title: "大檔案讀取：用 Grep 定位行號再 offset 讀取，不要整個讀進來"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [token效率, 工具使用]
date: 2026-04-01
still_relevant: true
permalink: /contributors/fishtvlvoe/021-efficient-file-reading/
---

# 大檔案讀取：用 Grep 定位行號再 offset 讀取，不要整個讀進來

## 問題

Claude 在需要查看一個大型檔案（>100 行）的某個特定部分時，直接整個讀進來——耗費大量 token，也讓 context 充滿無關代碼，降低後續推理品質。

例如：要查看一個 500 行的 PHP 檔案裡 `process_order` 函式的邏輯，卻把整個檔案都讀進來。

## 原因

Read 工具的預設行為是讀取整個檔案（或從頭開始的一段），Claude 如果沒有特別優化，會傾向用最直接的方式取得資料。

## 解決方案

對 >100 行的檔案，使用兩步驟策略：

**Step 1：用 Grep 定位目標的行號**

```bash
# 找函式定義
grep -n "function process_order" src/Plugin.php

# 找關鍵字在哪幾行
grep -n "ERROR\|Exception\|throw" src/Handler.php
```

**Step 2：用 Read 的 offset/limit 只讀需要的段落**

```
# 例如 grep 告訴你 process_order 在第 234 行
# 只讀 220-280 行的內容
Read(file, offset=220, limit=60)
```

這樣只消耗目標區段的 token，而不是整個檔案。

**什麼時候可以整個讀：**
- 檔案 ≤100 行
- 需要理解整個檔案的結構（第一次接觸時）
- 需要同時查看多個分散位置

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- 大檔案（>100 行）用 Grep 定位行號，再用 Read offset/limit 只讀需要的段落，不要整個讀進來。
```
