---
layout: default
title: "違反委派規則：自己動手而不外包給 Agent"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/013-delegation-bypass/
---

# 違反委派規則：自己動手而不外包給 Agent

## 問題

明明設定了清楚的 Agent 委派規則，Claude 還是直接在主對話親自做實作任務——寫代碼、改多個檔案、跑大型分析。

這讓主對話的 context window 被大量輸出塞滿，也違反了成本控制的初衷（主對話用 Opus/Sonnet，成本是 Copilot/cursor 的數十倍）。

更糟的是：路由規則明確寫在 CLAUDE.md，Claude 也說「我知道規則」，但下一步還是自己動手。這不是不知道規則，是反射性動手的習慣在規則之前觸發。

## 原因

Claude 有「立即執行」的強烈傾向，看到可以做的任務就會開始做。委派給其他 Agent 需要額外思考步驟，而直接執行感覺更快、更確定。

## 解決方案

在規則之外，加強「停頓檢查點」：

每次收到任務，在執行任何工具之前，必須先回答：
1. 「這超過 5 行代碼嗎？」→ YES → 停，選 Agent
2. 「這需要讀 3 個以上的檔案嗎？」→ YES → 停，選 Kimi
3. 「這是 UI/前端元件嗎？」→ YES → cursor-agent

寫「路由：XXX」這一行強迫自己外顯化決策，不讓反射性動手偷偷發生。

## 可複用的 CLAUDE.md 規則

```markdown
## 委派強制檢查點（每次收到任務，工具執行前必過）

回答以下問題，任一 YES → 停，選對應 Agent：
1. 超過 5 行代碼？ → Copilot / Kimi / Codex
2. 需讀 3 個以上檔案？ → Kimi MCP kimi_analyze
3. UI/前端元件？ → cursor-agent
4. 跨檔重構？ → Kimi CLI
5. 需要跑 shell 驗證？ → Codex

每次回應第一句話必須是：「路由：[判斷結果]」
全部 NO 才允許主對話直接執行
```
