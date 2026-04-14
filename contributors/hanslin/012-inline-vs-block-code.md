---
layout: default
title: "inline code 和 code block 的 CSS 會互相干擾"
parent: hanslin
grand_parent: 貢獻者
tags: [工具誤用, CLAUDE.md規則]
date: 2026-04-14
still_relevant: true
permalink: /contributors/hanslin/012-inline-vs-block-code/
---

# inline code 和 code block 的 CSS 會互相干擾

## 問題

Jekyll 的 Markdown 反引號 `code` 會產生 `<code class="language-plaintext highlighter-rouge">`。code block 的外層是 `<div class="highlighter-rouge">`。兩者共用 `.highlighter-rouge` class。

如果 CSS 用 `.highlighter-rouge { background: dark }` 設定 code block 的深色底，inline code 也會變成深色底，因為它也有 `.highlighter-rouge` class。

## 原因

Claude 沒注意到 inline code 和 code block 共用 class name。

## 解決方案

CSS selector 要用 `div.highlighter-rouge` 限定 code block，inline code 用 `code.highlighter-rouge` 單獨設定。如果 CSS 怎麼改都不生效，直接從 Markdown 源頭改（用粗體代替反引號）。

## 可複用的 CLAUDE.md 規則

```markdown
### Jekyll CSS
- code block 用 div.highlighter-rouge 限定，不要用 .highlighter-rouge
- inline code 的 class 是 code.language-plaintext.highlighter-rouge
- 兩者共用 class，CSS 必須分開處理
- CSS 改不動就從 Markdown 源頭改（粗體代替反引號）
```
