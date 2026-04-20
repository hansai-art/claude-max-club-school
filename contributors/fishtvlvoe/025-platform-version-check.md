---
layout: default
title: "加平台設定前先確認目標版本和限制"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [平台版本確認, 診斷不足]
date: 2026-04-01
still_relevant: true
permalink: /contributors/fishtvlvoe/025-platform-version-check/
---

# 加平台設定前先確認目標版本和限制

## 問題

Claude 在設定部署平台的設定檔時（Jekyll、GitHub Pages、Vercel、Netlify 等），會使用「最新版本」的語法或功能，沒有先確認目標平台實際支援的版本。

典型案例：GitHub Pages 使用 Jekyll 3.10，不是 Jekyll 4。Claude 如果直接用 Jekyll 4 的語法（例如某些 Liquid filter 或 `_config.yml` 選項），部署會靜默失敗或 build error，而本地測試卻沒問題（因為本地通常是較新版本）。

## 原因

Claude 的訓練資料偏向較新版本，對「平台鎖定在特定版本」這類限制，如果沒有明確詢問，容易忽略。

## 解決方案

**加任何平台相關設定之前，先確認版本：**

**GitHub Pages：**
```bash
# 查詢 GitHub Pages 當前支援的 Jekyll 版本
# 官方文件：https://pages.github.com/versions/
# 或查 dependency versions API
curl https://pages.github.com/versions.json
```

**Vercel / Netlify：**
```bash
# 確認 Node.js 版本
cat .node-version || cat .nvmrc

# 查 platform runtime 支援
# Vercel: Runtime 文件確認支援的 Node/Python/Ruby 版本
```

**一般原則：**
1. 不確定目標平台版本 → 查官方文件，不猜
2. 本地版本與平台版本不同 → 主動提醒用戶，建議對齊
3. 使用平台特定功能前 → 確認該版本是否支援

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- 加任何平台設定前先確認目標平台版本和限制（如 GitHub Pages 用 Jekyll 3.10 不是 4）。
  不確定就查官方文件，不要假設是最新版本。
```
