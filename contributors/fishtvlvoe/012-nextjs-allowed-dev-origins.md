---
layout: default
title: "Next.js 手機實機測試：allowedDevOrigins 設定"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [前端開發, 診斷不足]
date: 2026-05-04
still_relevant: true
permalink: /contributors/fishtvlvoe/012-nextjs-allowed-dev-origins/
---

# Next.js 手機實機測試：allowedDevOrigins 設定

## 問題

用手機或外部設備連 Next.js dev server（例如 `http://192.168.1.x:3000`），畫面一直卡在 loading skeleton，永遠不消失。

但用桌機開同一個網址完全正常，API 也正常回應，只是畫面不 hydrate。

## 原因

Next.js 16+ 的 dev server 有跨來源保護機制。手機用 LAN IP（如 `192.168.1.x`）連 dev server 時，CSS 和 JS 被跨來源保護擋住，導致 React hydration 失敗，所以 skeleton 永遠不消失。

症狀識別：
- API 正常回應（Network tab 的 API 請求是 200）
- HTML 有回（頁面有內容）
- 但 JS/CSS 被 blocked（Console 有跨來源錯誤）

## 解決方案

在 `next.config.ts` 加入 `allowedDevOrigins`：

```typescript
const nextConfig: NextConfig = {
  // ... 其他設定
  allowedDevOrigins: ['192.168.1.100'], // 換成你的手機/外部設備的 IP
}
```

加完之後重啟 dev server。

如果 LAN IP 會變動，可以用 CIDR 或直接允許整個子網路（視 Next.js 版本支援程度）。

## 可複用的 CLAUDE.md 規則

```markdown
## Next.js 手機/外部 IP 實機測試
- 症狀：API 正常、HTML 有回、但 skeleton 永遠不消失 → 優先懷疑跨來源保護
- 修法：next.config.ts 加 allowedDevOrigins: ['<LAN IP>'] 再重啟 server
- 適用：Next.js 16+，手機/外部設備用 LAN IP 連 dev server 的情況
```
