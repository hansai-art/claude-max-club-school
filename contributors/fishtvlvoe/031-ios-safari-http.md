---
layout: default
title: "iOS Safari 在 HTTP 環境下的靜默失敗：share 和 download 不動"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [iOS測試, 手機測試]
date: 2026-04-01
still_relevant: true
permalink: /contributors/fishtvlvoe/031-ios-safari-http/
---

# iOS Safari 在 HTTP 環境下的靜默失敗：share 和 download 不動

## 問題

在本機 `http://` 環境用 iPhone 測試時，兩個功能完全不動：
1. 「分享」按鈕按下去沒反應（`navigator.share()` 沒有出現系統分享選單）
2. 「儲存圖片」按鈕不觸發任何下載（`<a download>` 沒有開啟「儲存到相簿/檔案」彈窗）

Console 看到 `NotAllowedError`，或者靜默失敗什麼都沒有。

## 原因

iOS Safari 對部分 Web API 實施 **Secure Context 限制**，`http://` 不符合 Secure Context 要求（只有 `https://` 和 `localhost` 符合）：

- `navigator.share()` 在 HTTP 環境拋出 `NotAllowedError` 靜默失敗
- `<a download>` 在 HTTP 環境不觸發儲存行為，改為在新分頁打開圖片

**這不是代碼 bug。**

## 解決方案

**短期：** 這是預期行為，不需要修代碼。在本機 HTTP 測試看到這些現象是正常的。

**驗證：** 部署到 Vercel（或任何有 HTTPS 的平台）之後，這兩個功能會自動恢復正常運作。

**如果必須在本地測試：** 可以用 `mkcert` 建立本地 HTTPS：
```bash
brew install mkcert
mkcert -install
mkcert localhost 192.168.x.x
# 然後用 https://localhost:3000 或設定 dev server 使用 cert
```

**排查原則：** 遇到 `navigator.share()` 或 `<a download>` 在手機上靜默失敗，先確認當前 URL 是 `http://` 還是 `https://`，再決定是不是代碼問題。

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- iOS Safari 在 http:// 環境下：
  1. navigator.share() 拋 NotAllowedError 靜默失敗
  2. <a download> 不觸發儲存，改在新分頁開圖
  這是 Secure Context 限制，不是 bug。部署到 Vercel (HTTPS) 後自動修復，本機測試看到這些現象直接忽略。
```
