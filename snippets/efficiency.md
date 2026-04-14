---
layout: default
title: 效率規則
parent: 片段庫
nav_order: 1
permalink: /snippets/efficiency/
---

# 效率規則

減少 token 浪費、讓 Claude 一次做對的規則。**這裡是 canonical 版本**，其他頁面都連結到這裡。

---

## 工具使用優先順序

來源：[hanslin/001]({{ site.baseurl }}{% link contributors/hanslin/001-edit-not-write.md %})

```markdown
- Prefer Edit over Write for existing files：只送 diff，不重寫整檔
- 能用 Read 就不用 cat/head/tail
- 能用 Edit 就不用 sed/awk
- 能用 Grep 就不用 grep/rg
- 能用 Glob 就不用 find/ls
- Bash 只用在：shell script 執行、curl API、安裝套件、git 操作
```

---

## 診斷優先

來源：[hanslin/002]({{ site.baseurl }}{% link contributors/hanslin/002-diagnose-first.md %})

```markdown
- MUST 先列 2-3 個可能原因，讀 code 確認根本原因，才動手修
- 修法不 work 就 STOP 重新診斷，NEVER 在錯的方向疊 patch
- 失敗後先讀錯誤訊息，不要盲目重試
```

---

## 平行操作

來源：[hanslin/009]({{ site.baseurl }}{% link contributors/hanslin/009-parallel-tool-calls.md %})

```markdown
- 需要讀多個檔案時，一次送多個 Read，不要分多輪
- 需要同時跑 curl 和讀檔時，Bash + Read 平行送出
- 驗證多個 URL 時，一個 Bash 呼叫 for loop 全部檢查
- 研究類任務 dispatch 背景 agent，主線程繼續做不依賴結果的工作
```

---

## 精準讀取

來源：[hanslin/010]({{ site.baseurl }}{% link contributors/hanslin/010-read-only-what-you-need.md %})

```markdown
- 大檔案（>100 行）不要整個讀進來
- 先用 Grep 定位行號，再用 Read offset/limit 只讀那一段
- Write/Edit 完不要 Read 回來驗證，信任自己剛寫的內容
```

---

## 回應精簡

```markdown
- 直接講重點，不要開場白和結尾客套話
- 回答完就停，不加「還需要什麼嗎？」
```
