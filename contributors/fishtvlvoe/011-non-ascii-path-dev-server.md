---
layout: default
title: "中文路徑讓 Vite/Next.js Dev Server 白畫面"
parent: fishtvlvoe
grand_parent: 貢獻者
date: 2026-05-11
still_relevant: true
permalink: /contributors/fishtvlvoe/011-non-ascii-path-dev-server/
---

# 中文路徑讓 Vite/Next.js Dev Server 白畫面

## 問題

Vite 或 Next.js dev server 啟動正常，`localhost:3000` 打開後白畫面。API 回應正常，HTML 有內容，但 React/Vue 元件永遠不渲染。Console 沒有明顯 error，或出現 `@fs/...路徑` 中有 URL-encoded 中文字元（如 `2-顧問` → `2-%E9%A1%A7%E5%95%8F`）的奇怪請求。

真實案例：顧問案專案放在 `/Users/fishtv/Development/2-顧問/anismile/`，Medusa.js 後台（Vite）白畫面，`<div id="medusa">` 永遠空。移到 `/Users/fishtv/Development/clients/anismile/` 之後立刻正常。

## 原因

Node.js 在處理模組路徑時，會把中文字元 URL-encode。Vite/Next.js dev server 輸出的 `@fs/` URL 包含 encoded 中文路徑，瀏覽器請求這個 URL 時超時或被 dev server 拒絕，導致 JavaScript bundle 載入失敗，React/Vue 無法初始化。

**Symlink 救不了**：Node 會 resolve symlink 到真實路徑（readlink），真實路徑仍然含中文。

## 解決方案

**把整個專案實體搬家到全 ASCII 路徑**（用 `mv`，不是 `ln -s`）：

```bash
# 搬移整個專案到 ASCII 路徑
mv "/Users/fishtv/Development/2-顧問/anismile" "/Users/fishtv/Development/clients/anismile"

# 更新 IDE 書籤、shell alias 等
```

**預防**：新專案一律放在全 ASCII 路徑下。常見陷阱：
- `~/Development/1-個人/` — 有中文
- `~/Desktop/測試/` — 有中文
- `~/Documents/客戶案/` — 有中文

改成：
- `~/Development/personal/`
- `~/Desktop/test/`
- `~/Development/clients/`

## 可複用的 CLAUDE.md 規則

```markdown
### Vite/Next.js 路徑規則
- 專案路徑必須全 ASCII，不含中文、日文、韓文等非 ASCII 字元
- 非 ASCII 路徑 → @fs URL 被 encode → 模組載入失敗 → 白畫面，無明顯 error
- symlink 無效，Node 會 resolve 到真實路徑
- 修法：mv 整個專案到 ASCII 路徑（實體搬移，不是 ln -s）
- 症狀：API 正常、HTML 有回、但 React/Vue 元件永遠不渲染
```
