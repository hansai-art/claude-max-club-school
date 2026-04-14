# Claude MAX 俱樂部學校

> 送你的 Claude 來上學，讓它少犯別人已經踩過的坑。

[![瀏覽網站](https://img.shields.io/badge/📖_瀏覽網站-GitHub%20Pages-c15f3c)](https://hansai-art.github.io/claude-max-club-school/)
[![歡迎貢獻](https://img.shields.io/badge/🤝_歡迎貢獻-開始貢獻-2ea44f)](https://hansai-art.github.io/claude-max-club-school/getting-started/)
[![CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey)](LICENSE)

## 這是什麼？

我們是一群**台灣的 Claude MAX 用戶**。這裡不是理論教學，是**實戰踩坑紀錄**。

每一條規則都是某個人真的被 Claude 搞過之後寫下來的。你教會你的 Claude 一件事，100 個人的 Claude 都跟著學會。

## 三種用法

### 1. 讓你的 Claude 來學習

貼這段給你的 Claude Code，它會自動篩選跟你相關的規則：

```
去 https://github.com/hansai-art/claude-max-club-school

1. 先讀 _data/contributors.yml，找出技術棧跟我相近的貢獻者
2. 只讀那些相關貢獻者的經驗文章
3. 跳過 still_relevant: false 的過時規則
4. 把對我有用的 CLAUDE.md 規則整理出來
5. 直接幫我加進 ~/.claude/CLAUDE.md，跟既有規則去重
```

### 2. 裝新手懶人包（5 秒）

不想挑？直接裝[通用規則懶人包](https://hansai-art.github.io/claude-max-club-school/starter-pack/)，不管什麼技術棧都適用。

### 3. 貢獻你的經驗

貼這段給你的 Claude Code，它會自動整理你的踩坑紀錄並發 PR：

```
幫我貢獻經驗到 claude-max-club-school：

1. fork https://github.com/hansai-art/claude-max-club-school
2. 在 contributors/ 下建立我的資料夾（用我的 GitHub username）
3. 參考 contributors/_template/ 的格式，建立 index.md（個人簡介）
4. 讀取我的 ~/.claude/CLAUDE.md 和 memory 裡的 feedback 記錄，把所有踩坑經驗都整理成文章，越多篇越好
5. 每篇文章都要附上「可複用的 CLAUDE.md 規則」
6. push 後幫我發 PR
```

**進階：** 在 Claude Code 裡輸入 `/insight`，讓 AI 自動分析你的使用模式，挖出你沒注意到的問題，再貢獻上來。

## Repo 結構

```
_config.yml          # Jekyll 設定
_data/               # 機器可讀資料（contributors.yml）
_includes/           # HTML/CSS 覆蓋
contributors/        # 每人一個資料夾，放踩坑經驗
  _template/         # 新人複製這個開始
  hanslin/           # 示範：10 篇真實經驗
lessons/             # 按主題分類的索引
snippets/            # 可直接複製的 CLAUDE.md 規則（canonical 版本）
pages/               # 獨立頁面（懶人包、貢獻指南等）
index.md             # 首頁
```

## Badge

你的 Claude 在這裡上過學？在你的 README 加上：

```markdown
[![Claude School](https://img.shields.io/badge/🎓_Claude-在這裡上過學-c15f3c)](https://hansai-art.github.io/claude-max-club-school/)
```

[![Claude School](https://img.shields.io/badge/🎓_Claude-在這裡上過學-c15f3c)](https://hansai-art.github.io/claude-max-club-school/)

## 授權

[CC BY-SA 4.0](LICENSE)：自由使用、分享、修改，但要署名且以相同方式分享。

---

**English:** A crowd-sourced Claude Code knowledge base by Taiwan Claude MAX users. We share mistakes and lessons so everyone's Claude gets smarter. Traditional Chinese content, English contributions welcome.
