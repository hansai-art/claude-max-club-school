---
layout: default
title: "Next.js 手機實機測試：跨來源保護讓畫面永遠 loading"
parent: fishtvlvoe
grand_parent: 貢獻者
date: 2026-05-11
still_relevant: true
permalink: /contributors/fishtvlvoe/006-nextjs-mobile-dev-allowed-origins/
---

# Next.js 手機實機測試：跨來源保護讓畫面永遠 loading

## 問題

Next.js dev server 在本機跑好好的，手機用區網 IP（如 `http://192.168.x.x:3000`）連進來，畫面卡在 skeleton/loading，永遠不會消失。API 呼叫正常，HTML 有回應，但 React hydration 失敗。

## 原因

Next.js 16+ 加入了跨來源保護（cross-origin protection）。從 `localhost:3000` 以外的 origin 請求 CSS/JS 時，會被 dev server 阻擋，導致 React 無法 hydrate，畫面停在 server-rendered 的 skeleton 狀態。

這個保護機制本意是防止 DNS rebinding 攻擊，但副作用是手機實機測試完全無法進行。

## 解決方案

在 `next.config.ts`（或 `next.config.js`）加入 `allowedDevOrigins`：

```ts
// next.config.ts
const nextConfig = {
  experimental: {
    allowedDevOrigins: ['192.168.1.100'], // 換成你的機器 LAN IP
  },
}
export default nextConfig
```

加完後重啟 dev server（`npm run dev`），手機重新打開頁面。

**確認你的 LAN IP**：
```bash
# macOS/Linux
ifconfig | grep "inet " | grep -v 127.0.0.1
# 或
ip addr show | grep "inet " | grep -v 127.0.0.1
```

## 症狀辨識

- `localhost` 正常，手機/其他裝置用 IP 連進來一直 loading
- Network tab 顯示 HTML/API 200，但 CSS/JS 有問題或 console 有跨來源錯誤
- React DevTools 顯示 hydration 未完成

## 可複用的 CLAUDE.md 規則

```markdown
### Next.js 手機實機測試
- 手機連本機 dev server 畫面卡 loading → 優先懷疑跨來源保護
- 修法：next.config.ts 加 experimental.allowedDevOrigins: ['<LAN IP>']，重啟 server
- 症狀：API 正常、HTML 有回、但畫面卡在 loading skeleton
- 適用 Next.js 16+
```
