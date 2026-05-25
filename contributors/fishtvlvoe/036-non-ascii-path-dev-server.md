---
layout: default
title: "中文路徑讓 Vite/Next.js Dev Server 白畫面"
parent: fishtvlvoe
grand_parent: 貢獻者
date: 2026-05-11
still_relevant: true
permalink: /contributors/fishtvlvoe/036-non-ascii-path-dev-server/
---

# 中文路徑讓 Vite/Next.js Dev Server 白畫面

## 問題

Vite 或 Next.js dev server 啟動正常，打開 `localhost:3000` 後白畫面或 skeleton 永遠不消失。API 回應正常，HTML 有內容，但 React/Vue 元件永遠不渲染。

Console 可能出現含 URL-encoded 中文字元的奇怪路徑（如 `2-顧問` → `2-%E9%A1%A7%E5%95%8F`），或完全沒有錯誤訊息。

真實案例：顧問案專案放在 `/Users/fishtv/Development/2-顧問/anismile/`，Medusa.js 後台（Vite）白畫面，`<div id="medusa">` 永遠空。移到 `/Users/fishtv/Development/clients/anismile/` 之後立刻正常。

## 原因

Node.js 在處理模組路徑時，會把中文字元 URL-encode（`顧問` → `%E9%A1%A7%E5%95%8F`）。Vite/Next.js dev server 輸出的 `@fs/` 靜態資源 URL 會包含這個 encoded 路徑，瀏覽器請求時超時或被 dev server 拒絕，導致 JavaScript bundle 載入失敗，React/Vue 無法初始化。

**Symlink 救不了**：Node.js 會 resolve symlink 到真實路徑（readlink），真實路徑仍然含中文，問題依然存在。

## 解決方案

**把整個專案實體搬家到全 ASCII 路徑**（用 `mv`，不是 `ln -s`）：

```bash
# 搬移整個專案到 ASCII 路徑（實體搬移）
mv "/Users/fishtv/Development/2-顧問/anismile" "/Users/fishtv/Development/clients/anismile"

# 更新 IDE 書籤、shell alias 等
```

**常見的陷阱路徑（需要改名）**：

| 含中文的壞路徑 | 建議改為 |
|---|---|
| `~/Development/1-個人/` | `~/Development/personal/` |
| `~/Development/2-顧問/` | `~/Development/clients/` |
| `~/Desktop/測試/` | `~/Desktop/test/` |
| `~/Documents/客戶案/` | `~/Documents/projects/` |

**預防**：新專案建立時，目錄路徑從根到專案全部確認為 ASCII。

## 症狀辨識

- localhost 正常，但畫面 React 元件不渲染
- Network 面板看到 `@fs/` 請求失敗，URL 含 `%E...` 等中文 encode
- 或 Console 完全乾淨但畫面空白
- API endpoint 正常回應

以上同時出現 → 優先懷疑非 ASCII 路徑問題。

## 可複用的 CLAUDE.md 規則

```markdown
### Vite/Next.js 非 ASCII 路徑陷阱
- 專案路徑必須全 ASCII，不含中文、日文、韓文等非 ASCII 字元
- 症狀：API 正常、HTML 有回、但 React/Vue 元件永遠不渲染，無明顯 error
- 原因：@fs URL 被 URL-encode → 模組載入失敗 → hydration 失敗
- symlink 無效：Node 會 resolve 到真實路徑
- 修法：mv 整個專案到 ASCII 路徑（實體搬移，不是 ln -s）
- 適用：Vite、Next.js、Webpack 等前端 dev server
```
