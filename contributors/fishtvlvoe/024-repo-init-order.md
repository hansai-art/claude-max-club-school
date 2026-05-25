---
layout: default
title: "建立新 Repo 的正確初始化順序"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [專案初始化, CLAUDE.md規則]
date: 2026-04-01
still_relevant: true
permalink: /contributors/fishtvlvoe/024-repo-init-order/
---

# 建立新 Repo 的正確初始化順序

## 問題

Claude 在建立新 repo 時，有時會先寫業務代碼，再補 `.gitignore`、`LICENSE`、`README`；或者在 `package.json` / `requirements.txt` 裡用模糊的版本範圍（`^1.2.3`、`>=3.0`）而不是固定版本。

結果：
- 早期 commit 包含應該被忽略的檔案（node_modules、.env、build 產物）
- 依賴版本不固定，換環境或未來安裝時可能拿到不同版本，產生難以重現的 bug

## 原因

Claude 急於「解決問題」，傾向先寫功能代碼，把基礎設施（gitignore、license、固定版本）視為後置工作。這個順序看起來效率高，但實際上造成後患。

## 解決方案

建立新 repo 的正確初始化順序：

**第一步：基礎設施優先**
```bash
# 1. 建立 .gitignore（適合該專案類型）
# Node.js 專案
curl -o .gitignore https://raw.githubusercontent.com/github/gitignore/main/Node.gitignore

# 2. 選擇 LICENSE
# MIT、Apache-2.0 等，根據用途選擇

# 3. 建立 README.md（哪怕只有標題）

# 4. 第一個 commit 包含這三個
git add .gitignore LICENSE README.md
git commit -m "chore: initialize repository"
```

**第二步：固定依賴版本**
```json
// package.json - 固定版本，不用 ^ 或 ~
{
  "dependencies": {
    "react": "18.2.0",      // ✅ 固定版本
    "next": "14.1.0"        // ✅ 固定版本
    // "react": "^18.0.0"  // ❌ 不固定
  }
}
```

**第三步：才開始寫業務代碼**

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- 建 repo 後第一件事：.gitignore、LICENSE、README；
  依賴管理檔 MUST 固定版本（不用 ^ 或 ~），不要先寫內容再補基礎設施。
```
