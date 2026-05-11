---
layout: default
title: "Debug 403/500 前必須先看 server access log，不憑 DevTools 舊紀錄"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [診斷流程, Debug]
date: 2026-04-01
still_relevant: true
permalink: /contributors/fishtvlvoe/027-debug-server-log-first/
---

# Debug 403/500 前必須先看 server access log，不憑 DevTools 舊紀錄

## 問題

用戶貼出 DevTools console 的 403/500 錯誤截圖，Claude 立刻開始改代碼。結果：代碼改了沒用，因為那個錯誤其實是舊的——DevTools 保留的歷史 network 紀錄，部署早就修好了，只是用戶沒有強制刷新頁面。

## 原因

DevTools 的 Network tab 會保留 session 期間的所有請求，包括**部署前**發生的失敗請求。這些舊錯誤在 console 裡看起來和新錯誤一樣，很容易被當成「當前問題」。

## 解決方案

在 debug 任何 403/500 問題之前，MUST 先做以下確認：

**Step 1：SSH 查看 server access log**
```bash
# 查 access log 的最後幾筆
tail -n 50 ~/web/<site>/logs/<site>.log

# 確認 HTTP 狀態碼分布
awk '{print $9}' ~/web/<site>/logs/<site>.log | sort | uniq -c
```

**Step 2：比對時間戳**
- access log 最後一筆 403/500 是什麼時間？
- 部署完成是什麼時間？
- 如果部署後 log 全是 200 → 問題已修復，是 DevTools 舊紀錄

**Step 3：如果是 DevTools 舊紀錄**
```
告訴用戶：「Server log 顯示部署後全是 200，這是 DevTools 保留的舊錯誤。
請按 Cmd+Shift+R（Mac）或 Ctrl+Shift+R（Windows）強制刷新。」
```

**不要做：** 看到 console 有 403/500 就直接改代碼，沒有確認是否是當前發生的錯誤。

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- Debug 403/500 前 MUST 先 SSH 查 server access log，確認錯誤是「當下正在發生」還是「DevTools 保留的歷史紀錄」。
  比對 log 最後一筆時間 vs 部署完成時間。部署後 log 全是 200 → 叫用戶 Cmd+Shift+R 強制刷新，不要改代碼。
```
