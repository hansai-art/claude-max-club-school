---
layout: default
title: "只讀你需要的部分"
parent: hanslin
grand_parent: 貢獻者
tags: [token浪費, CLAUDE.md規則]
date: 2026-04-05
still_relevant: true
---

# 只讀你需要的部分

## 問題

Claude 要改檔案裡的某 3 行，卻把整個 500 行的檔案讀進來。文章 HTML 動輒 20K+ 字元，全部讀進來吃掉大量 context window。

## 原因

Claude 預設用 Read 工具時不指定 offset/limit，直接讀整個檔案。

## 解決方案

先用 Grep 定位行號，再用 Read 的 offset/limit 只讀需要的段落。

## 可複用的 CLAUDE.md 規則

```markdown
### 精準讀取
- 大檔案（>100 行）不要整個讀進來
- 先用 Grep 定位要改的位置（行號）
- 再用 Read offset/limit 只讀那一段
- 範例：Read file offset=170 limit=40（不是讀整個檔案）
- Write/Edit 完不要 Read 回來驗證，信任自己剛寫的內容
```
