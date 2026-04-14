---
layout: default
title: "CSS 改了不檢查就說修好了"
parent: hanslin
grand_parent: 貢獻者
tags: [盲目重試, 工作流程]
date: 2026-04-14
still_relevant: true
permalink: /contributors/hanslin/011-css-no-report-without-verify/
---

# CSS 改了不檢查就說修好了

## 問題

Claude 修改 CSS 後，看了一眼自己寫的 CSS 原始碼就說「修好了」。但 CSS 的實際渲染效果取決於瀏覽器的 selector 優先級、載入順序、繼承關係，光看原始碼判斷不了。

真實案例：修了 10+ 次 CSS 對比度問題，每次都說「修好了」，但使用者截圖顯示問題依舊存在。

## 原因

Claude 沒有瀏覽器，無法直接看到渲染效果。它傾向「寫完 = 修好」，跳過驗證步驟。

## 解決方案

推上去後必須用 curl 抓頁面 HTML，解析實際生效的 CSS 規則，確認對比度足夠才能回報。

## 可複用的 CLAUDE.md 規則

```markdown
### CSS 修改
- 改完 CSS 不能直接說「修好了」
- MUST 等 build 完成，curl 抓線上頁面驗證
- 檢查項目：每個元素的「背景色 + 文字色」在淺色和深色模式下是否可讀
```
