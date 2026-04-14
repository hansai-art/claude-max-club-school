---
layout: default
title: "不了解平台限制就加設定"
parent: hanslin
grand_parent: 貢獻者
tags: [診斷不足, CLAUDE.md規則]
date: 2026-04-14
still_relevant: true
permalink: /contributors/hanslin/025-permalink-pretty-fail/
---

# 不了解平台限制就加設定

## 問題

加了 `permalink: pretty` 想讓 URL 更乾淨，結果 build 失敗。因為 GitHub Pages 的 Jekyll 3.10 跟 Jekyll 4 的 permalink 行為不同。

同樣的問題也出現在設定 `color_scheme: default` 時，因為 jekyll-build-pages 的 sass load path 跟本地 Jekyll 不同。

## 原因

Claude 用 Jekyll 4 的知識來操作 Jekyll 3.10，沒有先確認版本差異。

## 解決方案

```markdown
### 平台限制
- 加任何設定前，先確認目標平台的版本和限制
- GitHub Pages 用 Jekyll 3.10，不是 Jekyll 4
- 不確定就查官方文件，不要猜
- 能用最簡單的方式就不要用進階功能
```
