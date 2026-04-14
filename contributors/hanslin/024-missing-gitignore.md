---
layout: default
title: "基本配置檔都忘了建"
parent: hanslin
grand_parent: 貢獻者
tags: [工具誤用, 工作流程]
date: 2026-04-14
still_relevant: true
permalink: /contributors/hanslin/024-missing-gitignore/
---

# 基本配置檔都忘了建

## 問題

初始化 Jekyll 專案時沒有建 `.gitignore`（排除 `_site/`、`.jekyll-cache/`），Gemfile 沒有固定版本號。都是被審查報告發現才補上的。

## 原因

Claude 急著寫內容，跳過了專案基礎設施。

## 解決方案

```markdown
### 新專案初始化
- 建 repo 後第一件事：.gitignore、LICENSE、README
- 依賴管理檔（Gemfile、package.json）MUST 固定版本
- 不要先寫內容再補基礎設施
```
