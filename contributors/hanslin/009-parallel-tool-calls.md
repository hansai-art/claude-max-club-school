---
layout: default
title: "平行呼叫工具省 token"
parent: hanslin
grand_parent: 貢獻者
tags: [token浪費, 工作流程]
date: 2026-04-05
still_relevant: true
permalink: /contributors/hanslin/009-parallel-tool-calls/
---

# 平行呼叫工具省 token

## 問題

Claude 需要讀 3 個檔案時，會分 3 輪各讀 1 個。需要驗證 7 個 URL 時，會分 7 輪各驗 1 個。每多一輪就多傳一次完整 context，token 消耗倍增。

在 64 sessions 的使用數據中，Bash 工具被呼叫了 3,126 次，很多是可以合併的操作。

## 原因

Claude 預設是「做一件事 → 回報 → 做下一件事」的循序模式。它不會主動思考「這幾件事可以同時做」。

## 解決方案

在 CLAUDE.md 裡明確指示平行操作的規則。

## 可複用的 CLAUDE.md 規則

```markdown
### 平行操作
- 需要讀多個檔案時，一次送多個 Read，不要分多輪
- 需要同時跑 curl 和讀檔時，Bash + Read 平行送出
- 驗證多個 URL 時，一個 Bash 呼叫 for loop 全部檢查
- 每省一輪 = 省一次完整 context 傳輸
- 研究類任務（找圖片、查資料）dispatch 背景 agent，主線程繼續做不依賴結果的工作
```
