---
layout: default
title: "內容專案用了程式碼授權"
parent: hanslin
grand_parent: 貢獻者
tags: [工具誤用, 工作流程]
date: 2026-04-14
still_relevant: true
permalink: /contributors/hanslin/023-wrong-license/
---

# 內容專案用了程式碼授權

## 問題

經驗分享的社群專案一開始用了 MIT License。MIT 是給程式碼的，不適合內容共創。

## 原因

Claude 預設建開源專案就用 MIT，沒有根據專案性質選擇授權。

## 解決方案

```markdown
### 授權選擇
- 程式碼專案：MIT 或 Apache 2.0
- 內容/文件專案：CC BY-SA 4.0
- 混合專案：程式碼 MIT + 內容 CC BY-SA
- 建專案時根據內容類型選擇，不要預設 MIT
```
