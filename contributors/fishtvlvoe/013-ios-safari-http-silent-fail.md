---
layout: default
title: "iOS Safari 在 http 環境的靜默失敗"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [前端開發, 診斷不足]
date: 2026-05-04
still_relevant: true
permalink: /contributors/fishtvlvoe/013-ios-safari-http-silent-fail/
---

# iOS Safari 在 http 環境的靜默失敗

## 問題

在 `http://` 環境下用 iPhone 測試，兩個功能神秘失效：

1. **分享功能**：`navigator.share()` 呼叫後什麼事都沒發生，Console 沒有 error
2. **圖片下載**：`<a download href="...">儲存圖片</a>` 點下去沒有出現「儲存到相簿」彈窗

在桌機 Chrome 一切正常，在 Android 手機也正常，只有 iOS Safari 有問題。

## 原因

iOS Safari 對這兩個功能有 HTTPS 要求：

- `navigator.share()` 在 `http://` 環境下拋出 `NotAllowedError`，但 iOS Safari 的行為是靜默失敗——不拋可見的 error，直接什麼都不做
- `<a download>` 在 `http://` 環境下不會觸發「儲存到相簿/檔案」的系統 dialog，而是在新分頁打開圖片

這不是 bug，是 iOS Safari 的安全設計。部署到 HTTPS 環境後（例如 Vercel）會自動恢復正常。

## 解決方案

本機 `http://` 測試看到這些現象：**不要修程式碼**。

應對方式：
1. 確認問題是否真的是 HTTPS 問題：在 Vercel 部署一版，用 HTTPS URL 測試
2. 如果 HTTPS 後正常 → 本機測試的限制，不需要修
3. 如果 HTTPS 後還是不正常 → 才是真正的 bug，再開始 debug

想在本機測 HTTPS，可以用 `ngrok` 或 `mkcert` 建立本機 HTTPS 環境。

## 可複用的 CLAUDE.md 規則

```markdown
## iOS Safari http 環境限制
- iOS Safari 在 http:// 環境：
  - navigator.share() → NotAllowedError 靜默失敗（不報 error）
  - <a download> → 不觸發儲存 dialog，改在新分頁開圖
- 這不是 bug，是 iOS Safari 安全限制，部署到 HTTPS 後自動修復
- 本機 http 看到這些現象：不動程式碼，部署到 Vercel/HTTPS 環境再驗
```
