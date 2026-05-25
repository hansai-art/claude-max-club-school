---
layout: default
title: "做完一個階段要主動告知下一步"
parent: fishtvlvoe
grand_parent: 貢獻者
date: 2026-05-11
still_relevant: true
permalink: /contributors/fishtvlvoe/003-proactive-next-step/
---

# 做完一個階段要主動告知下一步

## 問題

Claude 完成一個階段的工作後，直接停在那裡等用戶問「接下來呢？」。這讓用戶必須一直主動問，失去了 AI 助手的意義。

真實案例：Claude 完成了 Supabase migration，說「Migration 已完成」就沒了。Fish 必須再問「那前端要怎麼改？」Claude 說「要更新 TypeScript 型別」，Fish 再問「怎麼更新？」每個步驟都要 Fish 主動觸發，浪費大量來回時間。

## 原因

Claude 的預設模式是「完成任務，等待下一個指令」。它沒有意識到：多步驟任務中，用戶通常希望 Claude 主動帶著走，而不是每步都要推。

## 解決方案

每個階段完成後，主動輸出「下一步是什麼、需要用戶做什麼決定、我的建議是什麼」，並詢問是否繼續。

格式：「下一步是 X，需要你 Y，我的判斷是 Z，要繼續嗎？」

## 可複用的 CLAUDE.md 規則

```markdown
### 主動帶流程
- 每個階段完成後，MUST 主動告知：下一步是什麼、需要用戶做什麼決定、我的建議是什麼
- 格式：「下一步是 [X]，需要你 [Y]，我的判斷是 [Z]，要繼續嗎？」
- 禁止做完就停在那裡等用戶問「那接下來呢？」
- 不需要用戶判斷的步驟（測試通過、build 通過、commit）MUST 自動往下走，不等指令
```
