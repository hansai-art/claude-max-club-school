---
layout: default
title: "超過 5 行代碼就外包給外部 Agent"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/006-delegate-code-writing/
---

# 超過 5 行代碼就外包給外部 Agent

## 問題

Opus/Sonnet 在主對話親自寫大量代碼，消耗昂貴的 Anthropic token。

寫一個 100 行的函數、重構一個模組、生成測試套件——這些全部由主對話執行，cost 高且效率低。

## 原因

Claude 沒有把「規劃」和「執行」分開。主對話（大腦）的工作是決策和整合，具體的代碼撰寫應該外包給成本更低的外部工具。

在現代多模型協作環境中，有 Copilot CLI、Codex、cursor-agent 可以免費或低成本執行寫碼任務。

## 解決方案

收到寫碼任務，先問：「這要外包給哪個 Agent？」

分工依據：
- 核心業務邏輯 → Copilot CLI（免費）
- 需要讀大量 codebase + 改代碼 → Kimi CLI（大 context）
- 需要跑 shell / 測試驗證 → Codex CLI
- UI 元件 / scaffold → cursor-agent（零 token）
- 以上全失敗 → Sonnet 子代理（需說明原因）

主對話只做：規劃、決策、整合結果、1-2 行 hotfix。

## 可複用的 CLAUDE.md 規則

```markdown
## 代碼外包規則（強制）

超過 5 行程式碼 → 停，先問「哪個外部 Agent 最適合？」

分工：
- 業務邏輯/API/測試 → copilot -p "..." --yolo --model gpt-5.2
- 需讀大量 codebase 再改 → kimi -p "..." --yolo --print -w <dir>
- 需跑 shell/測試驗證 → codex exec "..."
- UI/scaffold → cursor-agent
- 以上全失敗 → Sonnet 子代理（說明原因）

主對話禁止：
- 親自寫超過 5 行代碼
- 親自讀 50+ 行檔案
- 親自做跨檔重構
- 看到寫碼任務就反射性動手
```
