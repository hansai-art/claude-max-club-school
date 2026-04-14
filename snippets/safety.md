---
layout: default
title: 安全規則
parent: 片段庫
---

# 安全規則

防止 Claude 搞壞你的東西。

---

## 檔案操作安全

```markdown
### 安全
- MUST `ls` before deleting any directory. NEVER `rm -rf` on dirs with user content.
- NEVER 修改 `.env` 以外的敏感檔案
- NEVER 執行 `sudo`、`rm -rf /`、`shutdown`、`reboot`、`mkfs`、`dd`
- NEVER 未經確認 force push
```

---

## 版本保護

```markdown
### 版本
- MUST 遞增版本號。NEVER 覆蓋舊版檔案。
```

**為什麼需要這條**：Claude 有時會直接覆蓋舊版本的檔案，導致無法回溯。

---

## 外部 API 覆蓋保護

```markdown
### 外部內容修改
- 修改已發布的內容（WordPress 文章、線上文件等）前，MUST 先從 API 拉取最新版本
- NEVER 用本地舊檔案覆蓋線上內容
- 流程：拉取 → 在最新版本上修改 → 推回
```

**真實案例**：用本地舊檔案覆蓋了 WordPress 文章，使用者在後台手動做的所有修改全部消失。

---

## 自動化腳本安全

```markdown
### 自動化腳本
- 偵測失敗後，MUST 先記錄實際狀態到 log 再決定是否重試
- NEVER 用同樣的邏輯盲目 retry
- Log 要記錄「期望值」和「實際值」
```
