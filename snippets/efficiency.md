---
layout: default
title: 效率規則
parent: 片段庫
---

# 效率規則

減少 token 浪費、讓 Claude 一次做對的規則。

---

## 工具使用優先順序

```markdown
## TOKEN DISCIPLINE

- Prefer Edit over Write for existing files — 只送 diff，不重寫整檔。
- Do not re-read files already read in this session unless content changed.
- 能用 Read 就不用 cat/head/tail
- 能用 Edit 就不用 sed/awk
- 能用 Grep 就不用 grep/rg
- 能用 Glob 就不用 find/ls
- Bash 只用在：shell script 執行、curl API、pip/npm 安裝、git 操作
```

**效果**：根據實測數據，Bash 佔工具使用的 50% 以上，其中大部分可以用專用工具替代。加上這條規則後 token 消耗明顯下降。

---

## 診斷優先

```markdown
### Diagnose Before Fixing
- MUST 先列 2-3 個可能原因，讀 code 確認根本原因，才動手
- 修法不 work，重新診斷，NEVER 疊 patch
- 失敗後不盲目重試，先讀錯誤訊息診斷原因
```

**效果**：消除「wrong approach」類型的浪費。在實測 64 sessions 中，73 次 wrong approach 是最大的 token 浪費源。

---

## 回應精簡

```markdown
## RESPONSE STYLE

- No sycophantic openers or closing fluff. 直接講重點。
- 回答完就停，不加「還需要什麼嗎？」「希望這有幫助」之類的廢話。
- Write 完不要 Read 驗證，信任自己剛寫的檔案。
```

**效果**：每次省下 1-3 輪來回，累積起來很可觀。
