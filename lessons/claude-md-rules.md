---
layout: default
title: CLAUDE.md 規則集
parent: 經驗分類
---

# CLAUDE.md 規則集

經過實戰驗證、可以直接複製貼上的 CLAUDE.md 規則。

每條規則都來自真實的踩坑經驗，不是理論建議。

---

## Token 效率

來源：[hanslin/001]({% link contributors/hanslin/001-edit-not-write.md %})

```markdown
- Prefer Edit over Write for existing files — 只送 diff，不重寫整檔。
- 能用 Read 就不用 cat/head/tail
- 能用 Edit 就不用 sed/awk
- 能用 Grep 就不用 grep/rg
- 能用 Glob 就不用 find/ls
```

---

## 診斷流程

來源：[hanslin/002]({% link contributors/hanslin/002-diagnose-first.md %})

```markdown
### Diagnose Before Fixing
- MUST 先列 2-3 個可能原因，讀 code 確認根本原因，才動手
- 修法不 work，重新診斷，NEVER 疊 patch
```

---

## 自動化腳本

來源：[hanslin/003]({% link contributors/hanslin/003-automation-debug.md %})

```markdown
### 自動化腳本的錯誤處理
- 偵測失敗後，MUST 先記錄實際狀態到 log
- NEVER 用同樣的邏輯盲目 retry
- Log 要記錄「期望找到什麼」和「實際找到什麼」
```

---

*歡迎貢獻你的 CLAUDE.md 規則。[開始貢獻]({% link getting-started.md %})*
