---
layout: default
title: "Build 通過不等於功能正確"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/038-build-pass-not-enough/
tags: [驗證, build, 行為測試, 功能正確]
date: 2026-05-18
still_relevant: true
---

# Build 通過不等於功能正確

## 問題

Claude 完成一個功能後，跑 `npm run build` 或 `tsc --noEmit` 通過就回報「完成」。

但 build 通過只代表：程式碼語法正確、型別沒有衝突。它**不**代表：

- 功能的輸出是對的
- API 回傳的格式是你預期的
- UI 在瀏覽器上實際渲染出來是正確的
- 邊界條件（空值、大資料量、併發）能正常處理

結果：用戶自己跑一次才發現功能根本壞的。這個問題在靜態型別語言（TypeScript、Rust）特別常見，因為 build 成功會給人一種「應該是對的」的錯覺。

## 原因

Build 是靜態驗證，快且不需要真實環境。Claude 傾向用最快的方式確認「有沒有明顯錯誤」，然後把球丟回給用戶。

這種行為有個常見偽裝說法：「你可以試跑一下看看是否符合需求。」實際上是把應該 Claude 做的驗證工作轉嫁給用戶。

## 解決方案

每個功能完成後，必須自己做**行為驗證**，依情境擇一：

**後端 / 純函式**

```bash
# 寫個小腳本用真實資料呼叫函式，確認輸出
node -e "
const { generateReport } = require('./src/reports');
const result = generateReport({ id: 1, items: [...] });
console.log(JSON.stringify(result, null, 2));
" > /tmp/test-output.json
cat /tmp/test-output.json
```

**API endpoint**

```bash
# 用 curl 實際打 API
curl -s http://localhost:3000/api/orders/1 | jq .
```

**UI 功能**

```bash
# 啟動 dev server，用 Playwright 截圖實際操作
npx playwright screenshot --full-page http://localhost:3000 /tmp/verify.png
```

輸出/截圖存到 `/tmp/` 供查閱，回報時附上「驗證了什麼、結果是什麼」。

## 可複用的 CLAUDE.md 規則

```markdown
## 功能驗證標準

- build 通過 ≠ 功能正確，禁止只跑 build 就回報「完成」
- 每個功能完成後 MUST 自己做行為驗證：
  - 純函式/後端邏輯：寫腳本用假資料呼叫，確認實際輸出
  - API：curl/fetch 打 endpoint，確認回傳格式正確
  - UI：dev server 跑起來 + 截圖每個畫面/狀態
- 驗證結果（輸出 JSON、截圖）存 /tmp/ 供用戶查閱
- 禁止說「你可以試跑一下確認」把驗證丟回給用戶
```
