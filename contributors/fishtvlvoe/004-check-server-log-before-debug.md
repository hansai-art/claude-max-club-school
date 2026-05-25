---
layout: default
title: "Debug HTTP 錯誤前先看 Server Log，不要憑 DevTools 舊紀錄動手"
parent: fishtvlvoe
grand_parent: 貢獻者
date: 2026-05-11
still_relevant: true
permalink: /contributors/fishtvlvoe/004-check-server-log-before-debug/
---

# Debug HTTP 錯誤前先看 Server Log，不要憑 DevTools 舊紀錄動手

## 問題

用戶把 DevTools console 的 403/500 錯誤截圖貼過來，Claude 看到就開始改代碼。但 DevTools 的 Network 面板會保留歷史紀錄，這些錯誤可能是 10 分鐘前、部署修復之前的舊紀錄。結果 Claude 在一個已經修好的問題上繼續亂改，反而引入新 bug。

真實案例：rsync 部署後 CSS/JS 回 403，Fish 把 DevTools 截圖給 Claude，Claude 開始改 `.htaccess` 和 Nginx 設定。但其實部署後 Claude 已經修復了權限問題，Server log 顯示最後幾分鐘全是 200，DevTools 顯示的 403 是部署前的快取紀錄。一個 `Cmd+Shift+R` 強制刷新就解決了。

## 原因

Claude 會直接相信用戶提供的錯誤截圖，沒有習慣先確認「這個錯誤現在還在發生嗎？」。DevTools 的視覺效果很有說服力，但它不是 real-time 的。

## 解決方案

debug HTTP 錯誤前，先 SSH 到 server 看 access log，確認錯誤是否「現在還在發生」：

```bash
# 看最近的 HTTP 狀態分布
tail -100 ~/web/<site>/logs/<site>.log | awk '{print $9}' | sort | uniq -c

# 看最後一筆各狀態的時間
grep ' 200 ' ~/web/<site>/logs/<site>.log | tail -3
grep ' 403 ' ~/web/<site>/logs/<site>.log | tail -3
```

判斷邏輯：
- 部署完成後 log 全是 200 → 問題已修復，叫用戶 `Cmd+Shift+R` 強制刷新
- Log 仍有 403/500 且時間在部署後 → 真實問題，才開始改代碼

## 可複用的 CLAUDE.md 規則

```markdown
### Debug HTTP 錯誤前必做
- 用戶貼 DevTools 403/500 → MUST 先 SSH 看 server access log
- 確認錯誤是「當下正在發生」還是「DevTools 保留的歷史紀錄」
- 判斷方式：比對 log 最後 403/500 的時間 vs 最後部署完成時間
- 部署後 log 全是 200 → 叫用戶 Cmd+Shift+R 強制刷新，不要動代碼
- 只有 log 確認現在仍有 5xx/4xx 才開始改
```
