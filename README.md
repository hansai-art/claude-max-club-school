# Claude MAX 俱樂部學校

[![Deploy](https://github.com/hansai-art/claude-max-club-school/actions/workflows/pages.yml/badge.svg)](https://github.com/hansai-art/claude-max-club-school/actions/workflows/pages.yml)
[![CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey)](LICENSE)
[![Contributors](https://img.shields.io/badge/Contributors-1-c15f3c)](_data/contributors.yml)
[![Lessons](https://img.shields.io/badge/Lessons-25-2ea44f)](https://hansai-art.github.io/claude-max-club-school/contributors/)

> 送你的 Claude 來上學，讓它少犯別人已經踩過的坑。

**[瀏覽網站](https://hansai-art.github.io/claude-max-club-school/)** ·
**[開始貢獻](https://hansai-art.github.io/claude-max-club-school/getting-started/)** ·
**[新手懶人包](https://hansai-art.github.io/claude-max-club-school/starter-pack/)** ·
**[Discussions](https://github.com/hansai-art/claude-max-club-school/discussions)**

---

## 為什麼需要這個？

我們是一群**台灣的 Claude MAX 用戶**。每天用 Claude Code 寫程式，也每天在踩坑。

每個人都在教自己的 Claude：寫 CLAUDE.md 規則、調提示策略、找更好的流程。但這些知識鎖在各自的電腦裡。

**這個 repo 把所有人的教訓集中起來。** 你教會你的 Claude 一件事，100 個人的 Claude 都跟著學會。

這裡不是理論教學，是實戰踩坑紀錄。每一條規則都是某個人真的被 Claude 搞過之後寫下來的。

## 快速開始

### 讓你的 Claude 來學習

貼這段給你的 Claude Code，它會根據你的背景自動篩選相關規則：

```
去 https://github.com/hansai-art/claude-max-club-school

1. 先讀 _data/contributors.yml，找出技術棧跟我相近的貢獻者
2. 只讀那些相關貢獻者的經驗文章
3. 跳過 still_relevant: false 的過時規則
4. 把對我有用的 CLAUDE.md 規則整理出來
5. 直接幫我加進 ~/.claude/CLAUDE.md，跟既有規則去重
```

懶得篩？直接裝[新手懶人包](https://hansai-art.github.io/claude-max-club-school/starter-pack/)，5 秒搞定。

### 貢獻你的經驗

貼這段給你的 Claude Code：

```
幫我貢獻經驗到 claude-max-club-school：

1. fork https://github.com/hansai-art/claude-max-club-school
2. 在 contributors/ 下建立我的資料夾（用我的 GitHub username）
3. 參考 contributors/_template/ 的格式，建立 index.md（個人簡介）
4. 讀取我的 ~/.claude/CLAUDE.md 和 memory 裡的 feedback 記錄
5. 把所有踩坑經驗都整理成文章，越多篇越好
6. 每篇文章都要附上「可複用的 CLAUDE.md 規則」
7. push 後幫我發 PR
```

也可以先在 Claude Code 裡輸入 **/insight**，讓 AI 自動分析你的使用模式，挖出你沒注意到的問題，再貢獻上來。

## 專案結構

```
claude-max-club-school/
├── _config.yml             # Jekyll 設定
├── _data/
│   └── contributors.yml    # 貢獻者索引（機器可讀）
├── _includes/
│   ├── head_custom.html    # CSS 主題覆蓋
│   └── footer_custom.html  # 深淺色切換按鈕
├── .github/
│   ├── workflows/          # CI：Pages 部署 + PR 驗證
│   ├── ISSUE_TEMPLATE/     # Issue 表單（分享經驗、我也遇過）
│   ├── CODEOWNERS          # 核心檔案保護
│   └── PULL_REQUEST_TEMPLATE.md
├── contributors/
│   ├── _template/          # 新貢獻者的範本
│   └── hanslin/            # 示範：25 篇實戰經驗
├── lessons/                # 按主題分類的索引
├── snippets/               # 可直接複製的 CLAUDE.md 規則
├── pages/                  # 獨立頁面（懶人包、貢獻指南等）
└── index.md                # 首頁
```

## 安全機制

- **PR 驗證 CI**：自動檢查檔案格式、安全掃描（擋腳本/XSS）、邊界檢查（只能改自己的資料夾）
- **Branch Protection**：必須走 PR + CI 通過 + 1 人 Review
- **CODEOWNERS**：核心設定檔只有維護者能改

## 技術棧

- [Jekyll](https://jekyllrb.com/) + [just-the-docs](https://just-the-docs.com/) 主題
- GitHub Pages 自動部署
- 支援深淺色模式切換
- 內建全站搜尋

## Badge

你的 Claude 在這裡上過學？

```markdown
[![Claude School](https://img.shields.io/badge/🎓_Claude-在這裡上過學-c15f3c)](https://hansai-art.github.io/claude-max-club-school/)
```

[![Claude School](https://img.shields.io/badge/🎓_Claude-在這裡上過學-c15f3c)](https://hansai-art.github.io/claude-max-club-school/)

## 授權

[CC BY-SA 4.0](LICENSE)

---

A crowd-sourced Claude Code knowledge base by Taiwan Claude MAX users. Traditional Chinese content, English contributions welcome.
