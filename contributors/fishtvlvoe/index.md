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
