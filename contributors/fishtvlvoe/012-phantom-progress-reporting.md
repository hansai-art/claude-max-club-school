---
layout: default
title: "幽靈進度：說完成但變更沒有持久化"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/012-phantom-progress-reporting/
---

# 幽靈進度：說完成但變更沒有持久化

## 問題

Claude 回報任務完成，但：
- 變更沒有 commit
- commit 了但沒有 push
- push 了但到錯誤的 branch
- Copilot/Agent 寫的檔案根本沒有持久化到磁碟

用戶以為完成了，下個 session 打開，發現什麼都不在。

真實案例：74 個任務的產品大改版，Claude 樂觀回報完成率，但 Copilot CLI 的 yolo 模式寫的檔案根本沒有持久化，實際完成率遠低於回報值。

另一個案例：emoji 改 SVG 的任務，Agent 回報完成，但變更沒有 push 到 main，用戶要指出兩次（手機和桌面版都還是 emoji）才找到問題。

## 原因

Claude 把「我已執行指令」等同於「任務完成」。但執行指令 ≠ 變更持久化 ≠ 部署到線上。在多 agent 協作環境中，各層都可能靜默失敗。

## 解決方案

任務完成前強制走完整驗證鏈：
1. `git status` — 確認 staged + committed
2. `git log --oneline -1` — 確認 commit 存在
3. `git push` 確認已推
4. 部署相關 — curl 線上 URL 或 API 回讀確認

每一步都要看到實際輸出，不要相信「我已執行」。

## 可複用的 CLAUDE.md 規則

```markdown
## 完成標準（任務完成前必做，強制）

標記任何任務為「完成」前，驗證鏈：
1. git status — 確認變更已 committed（不是只 staged）
2. 確認已 push 到正確 branch
3. 部署相關 — curl 線上 URL 或 API 回讀確認線上狀態
4. Spectra 任務 — 跑 validation，0 warnings 才算完

禁止：說「完成」但 git status 顯示有未 commit 的變更
禁止：樂觀回報 Agent/Copilot 的執行結果而不驗證持久化
```
