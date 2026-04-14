---
layout: default
title: "同樣內容寫了三份"
parent: hanslin
grand_parent: 貢獻者
tags: [工具誤用, 工作流程]
date: 2026-04-14
still_relevant: true
permalink: /contributors/hanslin/020-dry-violation/
---

# 同樣內容寫了三份

## 問題

貢獻指南的內容同時出現在 README.md、CONTRIBUTING.md、getting-started.md 三個地方。同一條 CLAUDE.md 規則在 7 個檔案裡重複出現。任何更新都要改 3-7 個地方，維護地獄。

## 原因

Claude 建檔案時沒有先規劃「哪裡是唯一來源」，每個檔案都獨立寫完整內容。

## 解決方案

```markdown
### DRY 原則
- 任何內容只能有一個 canonical 來源
- 其他地方用連結指向來源，不要複製內容
- 建新檔案前先問：這個內容是否已經存在？
```
