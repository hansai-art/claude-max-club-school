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
- **用 Claude Code 做什麼**：外掛開發、多模型 Agent 協作流程設計、自動化腳本、SDD（Spec-Driven Development）
- **使用的 Claude 方案**：Claude MAX
- **用了多久**：超過 6 個月，日均使用，建立了整套多模型協作路由規則

## 我的經驗文章

### 多模型協作與路由
- [工具不通先找替代，不說「沒辦法」](001-fallback-before-giving-up.md)：工具失敗時的靜默降級策略
- [任務完成主動報結果，不等被問](002-report-without-being-asked.md)：避免用戶焦慮等待

### Debug 與驗證
- [先診斷再動手，不要猜](003-diagnose-first-system.md)：系統性 debug 流程，避免反覆修錯
- [不確定的事自己查完再說](004-verify-before-speaking.md)：禁止把驗證工作推給用戶
- [任何任務開始前確認路徑、branch、環境](005-confirm-before-executing.md)：三確認防止改錯地方

### 工作流設計
- [超過 5 行代碼就外包給外部 Agent](006-delegate-code-writing.md)：主對話只做規劃和決策
- [重複操作必須自動化，不手動重複](007-automate-repetitive-tasks.md)：任何需要改 N 次的事都寫 script
- [推測必須標註「還沒驗證」](008-label-assumptions.md)：分清推測和事實，避免誤導用戶

### Spectra SDD 流程
- [每個任務強制三步：對齊→記錄→執行](009-three-step-task-discipline.md)：防止方向錯誤和無法追蹤
- [所有開發任務必須建立 Spectra Change](010-spectra-for-all-tasks.md)：SDD Loop 無例外，不允許只存在對話紀錄

### 高頻摩擦模式（來自 168 session 使用數據）
- [猜設定路徑浪費整個 session](011-guess-wrong-config-paths.md)：先讀實際檔案再動手，不憑記憶猜
- [幽靈進度：說完成但變更沒有持久化](012-phantom-progress-reporting.md)：git status + push 確認才算完
- [違反委派規則：自己動手而不外包給 Agent](013-delegation-bypass.md)：強制停頓檢查點，外顯路由判斷
- [能自己做的事，不要丟給用戶手動處理](014-do-it-yourself-not-user.md)：gh/git/CLI 能做的就自己做
- [解釋太技術性，用戶說「我看不懂」](015-over-technical-explanations.md)：預設白話文，技術細節按需給

### CLI 優先原則
- [Supabase 操作一律用 CLI，不開瀏覽器](016-supabase-cli-only.md)
- [Vercel 操作一律用 CLI，不開瀏覽器](018-vercel-cli-only.md)

### CSS 與前端
- [UI 按鈕禁用 Emoji，一律用 SVG Icon](017-svg-icons-not-emoji.md)
- [CSS 改動後必須線上驗證，改兩次沒好就停止診斷](019-css-online-verify.md)
- [覆蓋漸層元素必須同時清除 background-image 和 box-shadow](020-gradient-override.md)
- [UI commit 前必須截圖驗證每個畫面狀態](029-ui-screenshot-verify.md)
- [Next.js dev server 手機測試的 CORS 問題](030-nextjs-dev-cors.md)
- [iOS Safari 在 HTTP 環境下的靜默失敗](031-ios-safari-http.md)

### 效率與自動化進階
- [大檔案讀取：用 Grep 定位再 offset 讀取](021-efficient-file-reading.md)
- [自動化腳本失敗後先記錄實際狀態，才決定重試](022-automation-debug-log.md)

### Debug 進階
- [Debug 403/500 前必須先看 server access log](027-debug-server-log-first.md)

### 部署
- [rsync 部署完整 SOP：連線測試、chmod 修正權限](026-rsync-deploy-sop.md)

### 平台與整合
- [擴展點名稱必須查文件，不猜檔名](023-verify-extension-names.md)
- [建立 Repo 的正確初始化順序](024-repo-init-order.md)
- [加平台設定前先確認目標版本和限制](025-platform-version-check.md)

### React
- [React hook callback 的閉包陷阱：靜默失敗無錯誤](028-react-hook-closure.md)
