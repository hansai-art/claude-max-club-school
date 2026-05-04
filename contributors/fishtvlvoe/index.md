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

### 工具使用與效率
- [說「工具不能用」前先 `which X` 確認]({{ site.baseurl }}{% link contributors/fishtvlvoe/001-verify-tool-availability.md %})：別憑印象說工具不存在，先查再說
- [平台操作用 CLI，禁止叫用戶開瀏覽器]({{ site.baseurl }}{% link contributors/fishtvlvoe/007-cli-not-browser.md %})：Vercel/Supabase 都有 CLI，不叫用戶手動操作
- [Vercel env add 禁用 echo，用 printf 避免隱形 `\n`]({{ site.baseurl }}{% link contributors/fishtvlvoe/014-vercel-env-printf-not-echo.md %})：echo 帶換行符，外部 API 會拒絕，靜默失敗

### 診斷與驗證
- [不確定就自己查，禁止叫用戶「試試看」]({{ site.baseurl }}{% link contributors/fishtvlvoe/004-no-user-as-verifier.md %})：把驗證工作推給用戶是最常見的懶惰
- [Bug 診斷必須走完五步驟再告知]({{ site.baseurl }}{% link contributors/fishtvlvoe/005-bug-diagnosis-sop.md %})：蒐集→列因→排除→確認→修復→自驗→告知
- [debug 403/500 前必先看 server access log 時間戳]({{ site.baseurl }}{% link contributors/fishtvlvoe/009-check-server-log-first.md %})：DevTools console 的錯誤可能是歷史紀錄

### 自動化與工作流程
- [遇阻靜默試多方案，全失敗才回報]({{ site.baseurl }}{% link contributors/fishtvlvoe/002-silent-fallback-strategy.md %})：不要每個小障礙都打斷用戶
- [任何需要重複操作的事，必須自動化完成]({{ site.baseurl }}{% link contributors/fishtvlvoe/006-automate-dont-ask.md %})：把重複操作推給用戶是「名義完成，實際沒完成」
- [每個階段完成後主動告知下一步]({{ site.baseurl }}{% link contributors/fishtvlvoe/008-report-next-steps.md %})：不要做完就停在那裡等用戶問

### 前端開發（血淚教訓）
- [UI 按鈕圖示用 SVG，禁止 Emoji]({{ site.baseurl }}{% link contributors/fishtvlvoe/003-svg-not-emoji.md %})：Emoji 在不同平台渲染不一致，不是 UI 圖示
- [React hook callback 的閉包陷阱：靜默失敗無錯誤]({{ site.baseurl }}{% link contributors/fishtvlvoe/010-react-hook-stale-closure.md %})：功能不動 + Console 無 error = 優先懷疑 stale closure
- [UI 任務 commit 前必須截圖視覺驗證]({{ site.baseurl }}{% link contributors/fishtvlvoe/011-screenshot-before-ui-commit.md %})：grep 通過不代表渲染正確，截圖才是客觀證據
- [Next.js 手機實機測試：allowedDevOrigins 設定]({{ site.baseurl }}{% link contributors/fishtvlvoe/012-nextjs-allowed-dev-origins.md %})：跨來源保護擋住 CSS/JS，skeleton 永遠不消失
- [iOS Safari 在 http 環境的靜默失敗]({{ site.baseurl }}{% link contributors/fishtvlvoe/013-ios-safari-http-silent-fail.md %})：navigator.share() 和 download 需要 HTTPS，http 靜默失敗

### 資料庫
- [Postgres schema 演進用 ALTER TABLE，CREATE TABLE IF NOT EXISTS 是 no-op]({{ site.baseurl }}{% link contributors/fishtvlvoe/015-postgres-alter-not-create.md %})：表已存在時 CREATE TABLE IF NOT EXISTS 什麼都不做
