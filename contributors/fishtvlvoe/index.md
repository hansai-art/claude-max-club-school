---
layout: default
title: fishtvlvoe
parent: 貢獻者
has_children: true
---

# Fish（老魚）

## 關於我

- **身份**：一人公司經營者 / 獨立開發者
- **工作內容**：經營 BuyGo 電商管理系統（WordPress 外掛），台灣在地電商 SaaS
- **技術棧**：WordPress + PHP、Next.js + Supabase、多模型 AI 協作框架（GSD / Spectra）
- **用 Claude Code 做什麼**：外掛開發、多模型 Agent 協作流程設計、SDD（Spec-Driven Development）
- **使用的 Claude 方案**：Claude MAX
- **用了多久**：超過 6 個月，日均使用

## 我的經驗文章

### 工作流程與代理協作
- [叫用戶開瀏覽器操作等於白工]({{ site.baseurl }}{% link contributors/fishtvlvoe/001-no-browser-use-cli.md %})：Vercel/Supabase/GitHub 一律用 CLI
- [工具失敗不要馬上打斷用戶]({{ site.baseurl }}{% link contributors/fishtvlvoe/002-silent-fallback-before-report.md %})：靜默試備選方案，全失敗才回報
- [做完一個階段要主動告知下一步]({{ site.baseurl }}{% link contributors/fishtvlvoe/003-proactive-next-step.md %})：不要做完就停在那裡等用戶問
- [派工給外部代理前，先 git commit 所有未追蹤檔案]({{ site.baseurl }}{% link contributors/fishtvlvoe/008-git-commit-before-dispatch.md %})：git clean 會永久刪除 untracked 檔案

### 除錯技巧
- [Debug HTTP 錯誤前先看 Server Log]({{ site.baseurl }}{% link contributors/fishtvlvoe/004-check-server-log-before-debug.md %})：DevTools 快取紀錄不等於當前狀態
- [vercel env add 用 echo 會把換行字元存進去]({{ site.baseurl }}{% link contributors/fishtvlvoe/009-vercel-env-echo-newline.md %})：改用 printf，加完後 pull 驗證

### 資料庫
- [Postgres CREATE TABLE IF NOT EXISTS 不會升級既有的表]({{ site.baseurl }}{% link contributors/fishtvlvoe/010-postgres-create-table-no-upgrade.md %})：Schema 演進必須用 ALTER TABLE

### 前端開發陷阱
- [React Hook 回調裡不能呼叫 Hook 本身回傳的方法]({{ site.baseurl }}{% link contributors/fishtvlvoe/005-react-hook-callback-closure.md %})：閉包抓到舊值，靜默失敗無 error
- [Next.js 手機實機測試：跨來源保護讓畫面永遠 loading]({{ site.baseurl }}{% link contributors/fishtvlvoe/006-nextjs-mobile-dev-allowed-origins.md %})：設定 allowedDevOrigins
- [iOS Safari 在 HTTP 環境下的靜默失敗]({{ site.baseurl }}{% link contributors/fishtvlvoe/007-ios-safari-http-silent-fail.md %})：navigator.share 和 download 需要 HTTPS
- [中文路徑讓 Vite/Next.js Dev Server 白畫面]({{ site.baseurl }}{% link contributors/fishtvlvoe/011-non-ascii-path-dev-server.md %})：專案路徑必須全 ASCII
