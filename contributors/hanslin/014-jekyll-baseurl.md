---
layout: default
title: "Jekyll link 不會自動加 baseurl"
parent: hanslin
grand_parent: 貢獻者
tags: [工具誤用, CLAUDE.md規則]
date: 2026-04-14
still_relevant: true
permalink: /contributors/hanslin/014-jekyll-baseurl/
---

# Jekyll link 不會自動加 baseurl

## 問題

Jekyll 3.10（GitHub Pages 內建版本）的 `{% raw %}{% link page.md %}{% endraw %}` 產出的路徑不包含 `baseurl`。如果網站部署在 `github.io/project-name/`，所有連結都會 404。

75 個站內連結全部壞掉，按鈕點了都去錯誤頁面。

## 原因

Jekyll 4 的 `link` tag 會自動加 baseurl，但 GitHub Pages 用的是 Jekyll 3.10，不會自動加。Claude 假設了 Jekyll 4 的行為。

## 解決方案

所有 link 都要手動加 baseurl。

## 可複用的 CLAUDE.md 規則

```
### Jekyll on GitHub Pages
- GitHub Pages 用 Jekyll 3.10，不是 Jekyll 4
- link tag 必須寫成 site.baseurl + link page.md（用 Liquid 語法包裹）
- 不要假設 baseurl 會自動加
```
