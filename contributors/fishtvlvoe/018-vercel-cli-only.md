---
layout: default
title: "Vercel 操作一律用 CLI，不開瀏覽器"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [自動化原則, CLAUDE.md規則]
date: 2026-04-01
still_relevant: true
permalink: /contributors/fishtvlvoe/018-vercel-cli-only/
---

# Vercel 操作一律用 CLI，不開瀏覽器

## 問題

Claude 在需要操作 Vercel 時（例如設定環境變數、觸發部署），會叫用戶「去 Vercel Dashboard 打開 Settings > Environment Variables 加入這個值」。整個流程需要用戶切換瀏覽器、找到頁面、手動輸入，完全可以用 CLI 自動完成。

## 原因

Vercel Dashboard 的 UI 操作直觀易懂，Claude 習慣提供步驟說明。但當 Claude 有 terminal 存取權限時，這種說明是多餘的——直接做完才是正確行為。

## 解決方案

所有 Vercel 操作一律透過 CLI 執行：

**環境變數管理：**
```bash
# 新增環境變數
vercel env add MY_SECRET production

# 列出環境變數
vercel env ls

# 從 .env 批次設定
vercel env pull .env.local
```

**部署：**
```bash
# 部署到 preview
vercel

# 部署到 production
vercel --prod
```

**查看部署狀態：**
```bash
vercel ls
vercel inspect <url>
```

規則：Vercel CLI 能做到的事，Claude 自己執行完畢，不需要用戶開瀏覽器。

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- Vercel 操作一律用 CLI（vercel env / vercel deploy），不開瀏覽器、不叫用戶手動操作 Dashboard。
```
