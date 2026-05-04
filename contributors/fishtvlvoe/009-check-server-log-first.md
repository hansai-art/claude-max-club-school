---
layout: default
title: "debug 403/500 前必先看 server access log 時間戳"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [診斷不足, 後端開發]
date: 2026-05-04
still_relevant: true
permalink: /contributors/fishtvlvoe/009-check-server-log-first/
---

# debug 403/500 前必先看 server access log 時間戳

## 問題

用戶貼出 DevTools console 的 403 或 500 錯誤，Claude 馬上開始改程式碼、調設定。但這些錯誤其實是**部署前就存在的歷史紀錄**，部署後問題早就解決了。

結果：改了一堆沒必要改的東西，反而引入新問題。

## 原因

DevTools console 的錯誤會保留歷史紀錄，即使頁面重新整理，舊錯誤仍然顯示在 console 裡。Claude 看到錯誤就認為「現在有問題」，沒有確認這個錯誤發生的時間點。

## 解決方案

在根據任何 403/500 錯誤動手前，必須先：

1. SSH 到伺服器查 access log：
   ```bash
   tail -50 ~/web/<site>/logs/<site>.log
   ```
2. 統計當前 HTTP 狀態分布：
   ```bash
   awk '{print $9}' ~/web/<site>/logs/<site>.log | sort | uniq -c
   ```
3. 比對 access log 最後一筆 200 的時間 vs 部署完成時間

如果部署後的 log 全是 200，代表問題已解決，叫用戶 `Cmd+Shift+R` 強制重新整理，不要憑 console 舊紀錄動手改程式。

## 可複用的 CLAUDE.md 規則

```markdown
## 403/500 debug 前置步驟
- 用戶貼 DevTools 403/500 前，MUST 先 SSH 看 server access log 時間戳
- 確認錯誤是「當下正在發生」還是「部署前的歷史紀錄」
- 方法：比對 log 最後一筆時間 vs 部署完成時間
- 部署後若 log 全是 200 → 叫用戶 Cmd+Shift+R 強制刷新，不動程式碼
```
