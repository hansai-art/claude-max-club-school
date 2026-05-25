---
layout: default
title: "iOS Safari 在 HTTP 環境下的靜默失敗"
parent: fishtvlvoe
grand_parent: 貢獻者
date: 2026-05-11
still_relevant: true
permalink: /contributors/fishtvlvoe/007-ios-safari-http-silent-fail/
---

# iOS Safari 在 HTTP 環境下的靜默失敗

## 問題

在 `http://` 環境（本機測試）用 iOS Safari 測試時，某些功能完全不動，且沒有任何 error 訊息：

1. `navigator.share()` 拋出 `NotAllowedError`，但被吞掉，看起來像「按了沒反應」
2. `<a download>` 不觸發「儲存到相簿/檔案」彈窗，圖片直接在瀏覽器開啟

## 原因

iOS Safari 對部分 API 強制要求 HTTPS：
- Web Share API (`navigator.share()`) — 需要 secure context
- `<a download>` 下載行為 — 在 HTTP 下降級為在新分頁開啟

這些限制是 iOS 的安全政策，不是 bug，也不是代碼問題。在 Android Chrome 或桌面瀏覽器上不會遇到，只有 iOS Safari + HTTP 才會觸發。

## 解決方案

**本機測試看到這些現象不是 bug，部署到 Vercel/有 HTTPS 的環境後自動修復。**

如果需要在本機也測試這些功能，選項：
1. 用 `ngrok`/`cloudflared` 給本機 dev server 加 HTTPS tunnel
2. 直接部署到 Vercel preview URL 測試
3. 在 iOS Safari 設定裡暫時信任自簽憑證（麻煩，不推薦）

如果要做防禦性處理（讓 HTTP 下也能看到適當提示）：

```ts
// 分享前檢查是否支援
const handleShare = async () => {
  if (!navigator.share) {
    // HTTP 或不支援的瀏覽器，fallback
    await navigator.clipboard.writeText(url)
    toast('連結已複製')
    return
  }
  await navigator.share({ url })
}
```

## 可複用的 CLAUDE.md 規則

```markdown
### iOS Safari HTTP 限制
- iOS Safari 在 http:// 環境下：
  1. navigator.share() 拋 NotAllowedError 靜默失敗（看起來按了沒反應）
  2. <a download> 不觸發儲存，改在新分頁開圖
- 這不是 bug，部署到 HTTPS 後自動修復
- 本機 iOS 測試遇到這兩個現象：不要改代碼，改用 ngrok 或 Vercel preview
- 若需要 HTTP 相容：navigator.share 前加 if (!navigator.share) fallback
```
