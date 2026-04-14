# Claude MAX 俱樂部學校

> 送你的 Claude 來上學，讓它少犯別人已經踩過的坑。

[![GitHub Pages](https://img.shields.io/badge/Preview-GitHub%20Pages-blue)](https://hansai-art.github.io/claude-max-club-school/)
[![Contributors Welcome](https://img.shields.io/badge/Contributors-Welcome-green)](CONTRIBUTING.md)

## 這是什麼？

我們是一群**台灣的 Claude MAX 用戶**，每天用 Claude Code 寫程式、管網站、跑自動化。

這個 repo 是我們的共編經驗資料庫：

- **每個人有專屬資料夾**，放自己踩過的坑和學到的教訓
- **CLAUDE.md 片段庫**，可以直接複製貼上讓你的 Claude 變聰明
- **經驗按主題分類**，方便搜尋和瀏覽
- **GitHub Pages 預覽頁面**，不用 clone 也能瀏覽

## 為什麼要送你的 Claude 來上學？

你的 Claude 每天都在犯錯，你每天都在教它。但這些教訓都鎖在你的 CLAUDE.md 裡。

**Claude MAX 俱樂部學校讓所有人的教訓集中起來。** 你教會你的 Claude 一件事，100 個人的 Claude 都跟著學會。

這裡不是理論教學，是**實戰踩坑紀錄**。每一條規則都是某個人真的被 Claude 搞過之後寫下來的。

## 如何貢獻

三種方式，選最適合你的：

### 方式一：GitHub 網頁版（零安裝，推薦新手）

1. 點右上角 **Fork** 這個 repo
2. 在 `contributors/` 下建立一個以你 GitHub username 命名的資料夾
3. 複製 `contributors/_template/` 裡的範本到你的資料夾
4. 直接在 GitHub 網頁上編輯 Markdown
5. 點 **Commit changes** → **Create Pull Request**
6. 等待 review 後 merge，網站自動更新

### 方式二：本機操作

```bash
# Fork 後 clone
git clone https://github.com/你的帳號/claude-max-club-school.git
cd claude-max-club-school

# 建立你的資料夾
cp -r contributors/_template contributors/你的github帳號

# 寫你的經驗文章
# 編輯 contributors/你的github帳號/ 裡的檔案

# 推上去發 PR
git add .
git commit -m "feat: add lessons from 你的github帳號"
git push origin main
# 到 GitHub 發 Pull Request
```

### 方式三：開 Issue（最低門檻）

如果你不熟悉 Git，直接[開一個 Issue](../../issues/new/choose)，用表單填寫你的經驗，維護者會幫你建檔。

## 經驗文章格式

每篇文章使用這個結構：

```markdown
# 標題（描述 Claude 犯了什麼錯）

## 問題
（發生了什麼事，越具體越好）

## 原因
（為什麼 Claude 會這樣做）

## 解決方案
（你怎麼解決的）

## 可複用的 CLAUDE.md 規則
（可以直接貼進 CLAUDE.md 的片段）
```

## 預覽網站

[https://hansai-art.github.io/claude-max-club-school/](https://hansai-art.github.io/claude-max-club-school/)

## 授權

[MIT License](LICENSE) — 自由使用、分享、修改。

---

**What is this?** A crowd-sourced knowledge base by Taiwan Claude MAX users. We share our Claude Code mistakes and lessons learned, so everyone's Claude gets smarter together. [Start contributing](CONTRIBUTING.md).
