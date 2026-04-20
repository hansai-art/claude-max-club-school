---
layout: default
title: "自動化腳本失敗後先記錄實際狀態，才決定是否重試"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [自動化除錯, 診斷流程]
date: 2026-04-01
still_relevant: true
permalink: /contributors/fishtvlvoe/022-automation-debug-log/
---

# 自動化腳本失敗後先記錄實際狀態，才決定是否重試

## 問題

自動化腳本（批次處理、部署腳本、資料遷移等）失敗後，Claude 會直接用同樣的邏輯重試，而沒有先記錄是哪裡出問題。結果：重試也失敗，而且沒有有效的 debug 資訊，陷入「盲目 retry 循環」。

## 原因

Claude 在腳本失敗時，傾向「再試一次」的直覺反應，沒有先確認失敗的根本原因。對非確定性失敗（網路、lock 競爭）重試是合理的，但對於邏輯錯誤，重試只是浪費時間。

## 解決方案

腳本失敗後，MUST 先執行「狀態記錄」再決策：

**記錄格式（寫到 log 或 stderr）：**
```
[FAIL] 操作說明
  期望找到：<expected>
  實際找到：<actual>
  錯誤訊息：<error message>
  發生時間：<timestamp>
```

**決策邏輯：**
```python
try:
    result = do_operation()
except Exception as e:
    # 記錄實際狀態
    log(f"[FAIL] Expected: {expected}, Got: {actual}, Error: {e}")
    
    # 判斷是否值得重試
    if is_transient_error(e):  # 網路超時、rate limit
        retry_with_backoff()
    else:  # 邏輯錯誤、資源不存在
        raise  # 不重試，讓問題浮現
```

**禁止：** 失敗後不記錄任何狀態，直接用完全相同的邏輯 retry。這樣只是在重複同樣的錯誤。

**例子**：遷移腳本找不到某個 DB table → 先記錄「期望找到 orders_v2，實際找到 orders」→ 才決定是要修正 table 名稱還是先建立 table。

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- 自動化腳本失敗後 MUST 先記錄實際狀態（期望找到什麼 vs 實際找到什麼）到 log，
  才決定是否重試。禁止用同樣邏輯盲目 retry。
```
