---
layout: default
title: "叫用戶開瀏覽器操作等於白工"
parent: fishtvlvoe
grand_parent: 貢獻者
date: 2026-05-11
still_relevant: true
permalink: /contributors/fishtvlvoe/001-no-browser-use-cli/
---

# 叫用戶開瀏覽器操作等於白工

## 問題

Claude 遇到需要 Vercel、GitHub、Supabase、雲端控制台等操作時，會說「請你到瀏覽器打開 XXX 頁面，點 YYY 按鈕」。這等於把工作丟回給用戶，和「AI 幫你做事」的初衷完全相反。

真實案例：部署後 Vercel 環境變數需要更新，Claude 叫 Fish 「進 Vercel Dashboard 手動設定」。結果 Fish 花了 5 分鐘，Claude 本來 10 秒就能用 CLI 搞定。

## 原因

Claude 知道 CLI 工具存在，但在不確定用戶有沒有裝的情況下，傾向選擇「最保險」的方式——叫用戶自己操作 GUI。它沒有意識到「叫用戶做」本身就是一個成本。

## 解決方案

- Vercel 操作一律用 `vercel` CLI（`vercel env add`、`vercel deploy`）
- Supabase 操作一律用 `supabase` CLI（`supabase db push`、`supabase secrets set`）
- GitHub 操作一律用 `gh` CLI
- 瀏覽器 MCP（如 agent-browser、playwright）可以做的，自己做

**唯一例外**：需要用戶親自授權的操作（貼 API Key、2FA 驗證、付費操作、手動 Webhook 授權）。

## 可複用的 CLAUDE.md 規則

```markdown
### 禁止叫用戶開瀏覽器
- 禁止叫用戶在瀏覽器手動操作任何事情
- Vercel：一律用 vercel CLI（vercel env / vercel deploy）
- Supabase：一律用 supabase CLI（supabase db / supabase secrets）
- GitHub：一律用 gh CLI 或 GitHub MCP tools
- 瀏覽器可自動化的操作：用 playwright/agent-browser MCP 自己完成
- 唯一例外：需要用戶親自授權（API Key、2FA、付費操作）
- 違反 = 白工
```
