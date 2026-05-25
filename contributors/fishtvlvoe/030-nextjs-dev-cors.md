---
layout: default
title: "Next.js dev server 手機實機測試的 CORS 問題"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [Next.js, 手機測試]
date: 2026-04-01
still_relevant: true
permalink: /contributors/fishtvlvoe/030-nextjs-dev-cors/
---

# Next.js dev server 手機實機測試的 CORS 問題

## 問題

用手機或外部 IP 連到電腦的 Next.js dev server（`http://192.168.x.x:3000`）時，API 可以正常回應，HTML 也有回傳，但畫面卡在 skeleton loading 永遠不消失。Console 有 CORS 相關的 error，或者 React hydrate 失敗。

## 原因

Next.js 16+ 對 dev server 加入了跨來源保護（cross-origin protection）。當請求的 Origin（例如 `http://192.168.1.100:3000`）不在允許清單中時，CSS/JS 這些資源請求會被擋住，導致 React 無法 hydrate，skeleton 永遠停在那裡。

HTML 能回傳是因為 HTML 是 server render 的，但 JS bundle 和 CSS 被 CORS 擋了。

## 解決方案

在 `next.config.ts` 加入 `allowedDevOrigins`：

```typescript
// next.config.ts
import type { NextConfig } from 'next'

const nextConfig: NextConfig = {
  allowedDevOrigins: [
    '192.168.1.100',    // 你的 LAN IP
    '192.168.0.0/24',  // 或整個子網
  ],
}

export default nextConfig
```

加完之後重啟 dev server（`npm run dev`）。

**找到你的 LAN IP：**
```bash
# macOS/Linux
ifconfig | grep "inet " | grep -v 127.0.0.1

# Windows
ipconfig | findstr "IPv4"
```

**注意：** 這個設定只影響 dev 環境，production 部署到 Vercel/其他平台後不需要此設定。

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- Next.js 16+ 手機/外部 IP 連本機 dev server → CSS/JS 被跨來源保護擋住 → React hydrate 失敗 → skeleton 不消失。
  修法：next.config.ts 加 allowedDevOrigins: ['<LAN IP>'] 再重啟 server。
  症狀：API 正常、HTML 有回、但畫面卡在 loading。
```
