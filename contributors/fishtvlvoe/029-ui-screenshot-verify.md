---
layout: default
title: "UI commit 前必須截圖驗證每個畫面狀態，字串比對不夠"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [UI驗證, CLAUDE.md規則]
date: 2026-04-01
still_relevant: true
permalink: /contributors/fishtvlvoe/029-ui-screenshot-verify/
---

# UI commit 前必須截圖驗證每個畫面狀態，字串比對不夠

## 問題

UI 任務（HTML 原型、React 元件、CSS 改動）完成後，Claude 用 grep 確認「相關字串存在」就 commit，回報「已完成」。但實際在瀏覽器渲染的結果是錯的：

- Tab 切換後顯示錯誤的 content
- CSS 套用後 layout 跑版
- JavaScript toggle 邏輯有 bug

字串存在 ≠ 瀏覽器渲染正確。HTML 結構正確不代表 CSS/JS 邏輯也正確。

## 原因

Claude 沒有瀏覽器，容易把「代碼看起來對」當成「功能運作正確」。grep 驗證只能確認代碼存在，無法驗證行為正確性。

## 解決方案

**每個 UI 任務 commit 前 MUST 截圖驗證：**

**方法一：Playwright MCP**
```bash
# 啟動 dev server
npm run dev &

# 用 playwright 截圖每個畫面/狀態
playwright screenshot http://localhost:3000 /tmp/home.png
playwright screenshot http://localhost:3000/about /tmp/about.png
# 切換到每個 tab/modal/state 的截圖
```

**方法二：派工給子代理時，必須要求截圖**

當派工給 cursor-agent 或 Sonnet 子代理做 UI 任務時，prompt 結尾 MUST 加：

```
完成後用 playwright 截圖每個畫面/狀態存到 /tmp/，
把路徑列出，不要說「完成」，說「截圖在 X 請主對話驗證」。
沒有截圖 = 退回重做。
```

**驗證流程：**
1. Agent 回傳截圖路徑
2. 主對話 Read 截圖確認渲染正確
3. 有問題 → 退回 Agent 修正
4. 全部正確 → 才 commit

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- UI 任務（HTML 原型、React 元件、CSS 改動）commit 前 MUST 用 playwright 截圖驗證每個畫面/狀態。
  禁止「Agent 完成 + grep 字串存在」就 commit。字面驗證 ≠ 行為驗證。
- 派工給子代理做 UI 時，prompt 結尾 MUST 加截圖要求，沒截圖 = 退回重做。
```
