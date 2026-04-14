---
layout: default
title: "用了不存在的 include 檔名"
parent: hanslin
grand_parent: 貢獻者
tags: [診斷不足, CLAUDE.md規則]
date: 2026-04-14
still_relevant: true
permalink: /contributors/hanslin/021-wrong-include-name/
---

# 用了不存在的 include 檔名

## 問題

建了 `_includes/body_footer_custom.html` 想在頁面底部插入深色模式切換按鈕。但 just-the-docs 支援的是 `footer_custom.html`，不是 `body_footer_custom.html`。按鈕沒有出現。

## 原因

Claude 猜測了 include 的檔名，沒有先查文件確認。

## 解決方案

```markdown
### 使用第三方框架
- 要用 include/hook/slot 等擴展點前，MUST 先查文件確認正確名稱
- 不要猜檔名，just-the-docs 的 include 名稱是固定的
- 查文件的方式：curl 抓 GitHub raw 檔案或查官方文件
```
