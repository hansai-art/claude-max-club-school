---
layout: default
title: 新手懶人包
nav_order: 3
---

# 新手懶人包
{: .fs-8 }

不管你用什麼技術棧，這些規則都值得裝。
{: .fs-5 .fw-300 }

由社群投票選出、跨領域通用的 CLAUDE.md 規則。直接全部複製貼進你的 `~/.claude/CLAUDE.md` 就好。

---

## 一鍵安裝

把下面這段話貼給你的 Claude Code：

```
讀取 https://github.com/hansai-art/claude-max-club-school/blob/main/starter-pack.md
把裡面「完整懶人包」區塊的規則加進我的 ~/.claude/CLAUDE.md
如果已經有類似的規則就跳過，不要重複
```

---

## 完整懶人包

```markdown
## 工具使用

- Prefer Edit over Write for existing files — 只送 diff，不重寫整檔
- 能用 Read 就不用 cat/head/tail
- 能用 Edit 就不用 sed/awk
- 能用 Grep 就不用 grep/rg
- 能用 Glob 就不用 find/ls
- Bash 只用在：shell script 執行、curl API、安裝套件、git 操作

## 問題排查

- MUST 先列 2-3 個可能原因，讀 code 確認根本原因，才動手修
- 修法不 work 就 STOP 重新診斷，NEVER 在錯的方向疊 patch
- 失敗後先讀錯誤訊息，不要盲目重試

## 安全

- MUST ls before deleting any directory
- NEVER 用本地舊檔案覆蓋遠端內容，先拉最新版再改
- NEVER 未經確認 force push

## 自動化腳本

- 偵測失敗時 MUST 先記錄實際狀態到 log，再決定是否重試
- Log 要記「期望值」和「實際值」，方便事後比對
- NEVER 用同樣的邏輯盲目 retry

## 回應風格

- 直接講重點，不要開場白和結尾客套話
- 回答完就停，不加「還需要什麼嗎？」
```

---

## 這些規則怎麼來的？

| 規則 | 來源 | 驗證人數 |
|:-----|:-----|:--------|
| 用 Edit 不要用 Write | [hanslin/001]({% link contributors/hanslin/001-edit-not-write.md %}) | 1 |
| 先診斷再動手 | [hanslin/002]({% link contributors/hanslin/002-diagnose-first.md %}) | 1 |
| 自動化腳本當場記錄 | [hanslin/003]({% link contributors/hanslin/003-automation-debug.md %}) | 1 |

驗證人數 = 多少個貢獻者獨立發現同樣的問題。數字越高，代表越普遍。

---

*覺得某條規則應該加入懶人包？[發 PR](https://github.com/hansai-art/claude-max-club-school/pulls) 更新這個頁面。*
