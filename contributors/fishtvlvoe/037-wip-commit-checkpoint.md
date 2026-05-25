---
layout: default
title: "長任務一定要建 WIP 存檔點"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/037-wip-commit-checkpoint/
tags: [git, 多步任務, 存檔點, 自動化]
date: 2026-05-18
still_relevant: true
---

# 長任務一定要建 WIP 存檔點

## 問題

Claude 執行超過 3 個子步驟的長任務時，做完每一步後直接繼續下一步，不做任何 commit。

結果：

- 對話被 compact（壓縮）後，Claude 忘記前幾步做了什麼
- 中途派出外部代理（Copilot CLI、Cursor 等）時，代理執行 `git clean` 或 `git restore` 把所有 untracked 工作永久刪除
- Session 意外中斷後什麼都不剩，只能從頭來過

## 原因

Claude 把「對話 history」當成工作備份。但對話 history 不是 git，有三種情況會讓它失效：

1. **Context compaction**：長對話的前段被自動壓縮，細節消失
2. **外部代理破壞**：`git clean -fd` 把所有 untracked 檔案永久刪除，`git reflog` 也救不回
3. **Session 中斷**：網路斷線或超時，未 commit 的工作歸零

## 解決方案

每完成一個邏輯子步驟，立刻做 WIP commit：

```bash
git add -A && git commit -m "wip: <子步驟名稱>"
```

例如「新增會員系統」任務可以分解為：

```
wip: schema migration done
wip: auth API endpoints done
wip: frontend login form done
wip: integration tests pass
```

判斷何時要建存檔點：
- 超過 3 個子步驟的任務 → 每步結束就 commit
- 準備派外部代理執行前 → 必須先 commit（見 035-git-commit-before-dispatch）
- 跨越不同技術邊界（後端 → 前端、API → DB）時

不做 commit 就不算開始下一步。

## 可複用的 CLAUDE.md 規則

```markdown
## 長任務存檔點策略

- 超過 3 個子步驟的任務，每個子步驟結束後 MUST 立即執行 `git add -A && git commit -m "wip: <步驟名稱>"`
- 對話 history 不是 git，不能依賴對話記憶當備份
- 準備派外部代理前 MUST 先 commit，確保沒有 untracked 重要檔案
- 一個子步驟做完不 commit 就不算開始下一步
```
