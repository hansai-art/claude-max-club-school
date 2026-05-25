---
layout: default
title: "所有開發任務必須建立 Spectra Change，不只存在對話中"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/010-spectra-for-all-tasks/
---

# 所有開發任務必須建立 Spectra Change，不只存在對話中

## 問題

開發任務在對話裡討論、執行、完成，但沒有任何文件記錄下來。

下一個 session 打開，「我們上次做到哪裡？」——找不到，因為在 context 裡，context 壓縮後消失了。

更糟的是：bug 出現了，「為什麼這樣寫？」——找不到當初的設計決策。

## 原因

對話感覺比文件更快，不需要切換工具。但對話是揮發性的，文件才是持久性的。

當只有一個人、一個 session 的時候，對話夠用。當有多個 session、多個模型協作、或者隔天回來繼續的時候，對話不夠用。

## 解決方案

採用 Spec-Driven Development（SDD）流程：

每個開發任務建立一個 Spectra Change，包含：
- `proposal.md`：目標、設計決策、邊界
- `design.md`：技術方案、Agent 分工
- `tasks.md`：可執行的任務清單，每個標註 `[Tool: xxx]`

執行完才標 `[x]`，不是「做了」就標。

有 Change 之後，跨 session 只需要說「繼續 Change X」，新的 session 直接讀文件接手。

## 可複用的 CLAUDE.md 規則

```markdown
## Spectra SDD 強制規則

所有執行類任務必須先建立 Spectra Change（或更新現有 Change）：
- 修 bug / debug → 必須有 Change
- 加功能 / 新需求 → 必須有 Change
- 重構 / 架構調整 → 必須有 Change
- 1 行 hotfix → 唯一例外，但要在對應 Change 的 tasks.md 記錄

流程：
1. 收到任務 → 判斷有沒有現有 Change
2. 有 → 更新 Change（ingest）
3. 沒有 → 建新 Change（propose）
4. 才開始執行

執行完才標 [x]，不允許只存在對話紀錄。
```
