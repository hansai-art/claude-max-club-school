---
layout: default
title: "猜設定路徑浪費整個 session"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/011-guess-wrong-config-paths/
---

# 猜設定路徑浪費整個 session

## 問題

Claude 要設定某個工具（MCP、CLI、設定檔），沒有先讀實際檔案，直接憑記憶猜路徑。猜錯一個，改一個，再猜，再改——最後整個 session 耗在找正確路徑上，原本要做的事一件都沒做。

真實案例：要設定 Stitch MCP，Claude 依序試了 `settings.json`、`.mcp.json`、其他錯誤位置，最後才發現正確方法是 `claude mcp add -s user`。到那時候 session 已經耗盡。

另一個案例：跨多個 session 反覆猜錯 Kimi K2.6 的 model ID，最後才發現 CLI 根本不支援切換 model——用了兩個 session 在一件做不到的事上。

## 原因

Claude 的訓練資料包含大量「常見配置」的知識，容易在沒有讀實際檔案的情況下直接使用。但每個用戶的環境不同，猜測必然失敗。

## 解決方案

設定任何工具前，強制先讀：
1. 實際的設定檔（`cat ~/.claude/mcp.json`、`cat ~/.claude/settings.json`）
2. CLI help（`<tool> --help`、`<tool> --list-models`）
3. 現有結構（`ls openspec/changes/`）

讀完確認了再動手，不憑記憶。

## 可複用的 CLAUDE.md 規則

```markdown
## 設定路徑先讀後用（強制）

使用任何工具/MCP/CLI 的設定前，先讀實際檔案確認，不憑記憶猜測：
- MCP 設定：cat ~/.claude/mcp.json
- CLI 支援的 flag/model：<tool> --help
- 專案結構：ls <目錄> 確認現有檔案

禁止：猜一個路徑、失敗、再猜另一個
禁止：假設某個 CLI flag 存在而不先驗證
```
