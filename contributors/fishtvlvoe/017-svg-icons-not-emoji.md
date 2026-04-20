---
layout: default
title: "UI 按鈕禁用 Emoji，一律用 SVG Icon"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [UI設計, CLAUDE.md規則]
date: 2026-04-01
still_relevant: true
permalink: /contributors/fishtvlvoe/017-svg-icons-not-emoji/
---

# UI 按鈕禁用 Emoji，一律用 SVG Icon

## 問題

Claude 在設計 UI 元件時，偶爾會用 Emoji 當圖示：例如按鈕上放 ✉️、🔔、⚙️。這在原型階段看起來方便，但在實際產品中會產生跨平台渲染不一致、大小難以控制、無障礙支援差等問題。

## 原因

Emoji 在 Markdown 或純文字說明中很直觀，Claude 在生成 UI 代碼時容易沿用這個習慣。此外，Emoji 不需要額外引入 icon library，看起來「省事」。

## 解決方案

所有 UI 按鈕、圖示一律使用 SVG icon library：

**推薦 library：**
- [Heroicons](https://heroicons.com/)（Tailwind 官方維護，React/SVG 支援）
- [Lucide](https://lucide.dev/)（Feather icons 繼承者，輕量）

**使用方式（以 Heroicons 為例）：**

```tsx
import { BellIcon, CogIcon } from '@heroicons/react/24/outline'

// 代替 🔔
<BellIcon className="h-5 w-5" />

// 代替 ⚙️
<CogIcon className="h-5 w-5" />
```

**純 HTML 專案**：直接內嵌 SVG 字串，或從 Heroicons 網站複製 SVG 代碼。

SVG icon 的優點：大小可控（className/style）、顏色跟隨 currentColor、無障礙加 aria-label 容易、跨平台渲染一致。

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- UI 按鈕、圖示一律用 SVG icon（Heroicons / Lucide），禁止用 Emoji 當 UI 元素。
  React 專案用 @heroicons/react 或 lucide-react，純 HTML 直接內嵌 SVG。
```
