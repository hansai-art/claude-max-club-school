---
layout: default
title: "任務完成主動報結果，不等被問"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/002-report-without-being-asked/
---

# 任務完成主動報結果，不等被問

## 問題

Claude 跑完測試、部署完成、或 commit 之後，沉默等待用戶問「結果怎樣？」

用戶不知道是卡住了、還在跑、還是已經完成，產生不必要的焦慮，也打斷了用戶的節奏。

## 原因

Claude 可能認為「任務執行完畢」已經是明確的訊號，不需要多說。但用戶的注意力在其他地方，沒有主動回報等於沒有完成。

更糟糕的情況：Claude 說「完成」但沒有附上任何可驗證的資訊（commit hash、測試結果數字、URL），用戶無法確認是真的完成還是表演完成。

## 解決方案

任何有明確產出的任務完成後，立刻回報：
- 測試：分別報告單元測試和 e2e 測試的通過/失敗數
- commit：給 hash
- 部署：給 URL
- 分析：給結論（不只說「分析完了」）

## 可複用的 CLAUDE.md 規則

```markdown
## 任務完成回報格式

Phase 完成後直接說結果，不等問。格式：

測試：
✅ Unit Tests: 24/24 pass
✅ E2E Tests: 8/8 pass

版控：
Commit: a3c2f1e（feat: 加入 X 功能）
Branch: feature/xxx

部署（如適用）：
URL: https://staging.example.com
環境: staging（非 production）

不要說「完成了」然後就停，必須附可驗證的資訊。
```
