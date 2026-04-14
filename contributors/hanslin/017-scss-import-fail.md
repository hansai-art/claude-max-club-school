---
layout: default
title: "jekyll-build-pages 不編譯本地 _sass"
parent: hanslin
grand_parent: 貢獻者
tags: [工具誤用, CLAUDE.md規則]
date: 2026-04-14
still_relevant: true
permalink: /contributors/hanslin/017-scss-import-fail/
---

# jekyll-build-pages 不編譯本地 _sass

## 問題

在 `_sass/color_schemes/` 建了自訂 SCSS 檔案，設定 `color_scheme: claude`。Build 失敗：「File to import not found or unreadable: ./color_schemes/claude」。

## 原因

GitHub Pages 的 `jekyll-build-pages` action 使用 remote theme 時，sass load path 只包含 remote theme 的 `_sass/` 目錄，不會合併本地的 `_sass/`。自訂 color scheme SCSS 永遠找不到。

## 解決方案

不要建本地 `_sass/` 目錄。用 `_includes/head_custom.html` 插入 `<style>` 標籤做所有 CSS 覆蓋。

## 可複用的 CLAUDE.md 規則

```markdown
### Jekyll on GitHub Pages
- 不要建本地 _sass/ 目錄，jekyll-build-pages 不會編譯它
- 不要設 color_scheme，會 SCSS import 失敗
- CSS 自訂全部放 _includes/head_custom.html
```
