---
layout: default
title: "CSS 改動後必須線上驗證，改兩次沒好就停止診斷"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [CSS驗證, 診斷流程]
date: 2026-04-01
still_relevant: true
permalink: /contributors/fishtvlvoe/019-css-online-verify/
---

# CSS 改動後必須線上驗證，改兩次沒好就停止診斷

## 問題

兩個相關但常一起出現的 CSS 壞習慣：

1. **改完 CSS 就說「修好了」**：Claude 在改完 HTML/CSS 後，只看原始碼確認改動存在，就宣告完成——但沒有確認瀏覽器實際渲染的結果。
2. **疊加 patch 而不診斷根因**：CSS 改了一次沒效果，再改第二次，再試第三次，越改越複雜，但都沒有回頭找真正的問題在哪裡。

## 原因

Claude 沒有瀏覽器，容易把「代碼改動存在」等同於「問題已修復」。CSS 的特殊性在於：樣式優先級（specificity）、繼承、瀑布效果讓代碼正確不代表渲染正確。疊加 patch 是一種「試錯」心態，每次改一點希望能碰對，但缺乏系統性診斷。

## 解決方案

**規則一：CSS 改完 MUST 用 curl/fetch 抓線上頁面驗證**

```bash
# 驗證頁面回應
curl -s https://yoursite.com/page | grep "target-class"

# 檢查 CSS 是否正確載入
curl -s https://yoursite.com/style.css | grep "target-property"
```

如果是本地開發，用 `curl localhost:PORT` 確認實際 HTML 輸出。不能只看原始碼就說「修好了」。

**規則二：CSS 改兩次沒修好 → STOP，系統性診斷**

第一次改沒效果，第二次改也沒效果，這時不要繼續猜——改做根因診斷：

```bash
# 抓取 theme CSS，找出影響目標元素的所有 rule
curl -s https://yoursite.com/style.css > /tmp/theme.css
grep -n "target-selector" /tmp/theme.css
```

列出所有影響目標元素的 CSS rule，分析 specificity 衝突，找出真正需要覆蓋的規則，才繼續動手改。

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- CSS/HTML 改完 MUST 用 curl/fetch 抓線上頁面驗證，不能只看原始碼就說「修好了」。
- CSS 改兩次沒修好 → STOP，curl 抓 theme CSS，列出影響目標元素的所有 rule 再診斷，不要繼續疊 patch。
```
