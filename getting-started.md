---
layout: default
title: 開始貢獻
nav_order: 2
---

# 開始貢獻
{: .fs-8 }

三種方式，選最適合你的。
{: .fs-5 .fw-300 }

---

## 方式一：GitHub 網頁版（零安裝）
{: .text-green-300 }

**適合**：不熟 Git 的人、想快速貢獻一篇的人

### 第 1 步：Fork 這個 Repo

1. 到 [GitHub Repo 頁面](https://github.com/hansai-art/claude-max-club-school)
2. 點右上角的 **Fork** 按鈕
3. 保持預設設定，點 **Create fork**

### 第 2 步：建立你的資料夾

1. 在你 fork 的 repo 裡，進入 `contributors/` 資料夾
2. 點 **Add file** → **Create new file**
3. 在檔名欄位輸入 `你的GitHub帳號/index.md`（例如 `johndoe/index.md`）
4. 這會自動建立資料夾

### 第 3 步：寫你的個人簡介

把以下內容貼進 `index.md`，改成你的資料：

```markdown
---
layout: default
title: 你的GitHub帳號
parent: 貢獻者
has_children: true
---

# 你的名字

簡單介紹自己，例如：
- 用 Claude Code 多久了
- 主要用來做什麼
- 踩過最深的坑是什麼
```

### 第 4 步：寫你的第一篇經驗

1. 在你的資料夾裡，點 **Add file** → **Create new file**
2. 檔名格式：`001-簡短描述.md`（例如 `001-dont-use-write.md`）
3. 用以下範本：

```markdown
---
layout: default
title: "你的經驗標題"
parent: 你的GitHub帳號
grand_parent: 貢獻者
---

# 你的經驗標題

## 問題
（Claude 犯了什麼錯？越具體越好）

## 原因
（為什麼會這樣？）

## 解決方案
（你怎麼解決的？）

## 可複用的 CLAUDE.md 規則
把這段貼進你的 CLAUDE.md：
（可以直接複製的規則）
```

### 第 5 步：發 Pull Request

1. 回到你 fork 的 repo 首頁
2. 會看到提示 "This branch is X commits ahead"
3. 點 **Contribute** → **Open pull request**
4. 填寫標題和說明，點 **Create pull request**
5. 等待 review 後 merge！

---

## 方式二：本機操作
{: .text-blue-300 }

**適合**：熟悉 Git 的開發者

```bash
# 1. Fork 後 clone
git clone https://github.com/你的帳號/claude-max-club-school.git
cd claude-max-club-school

# 2. 建立你的資料夾（從範本複製）
cp -r contributors/_template contributors/你的帳號

# 3. 編輯檔案
#    - contributors/你的帳號/index.md  （個人簡介）
#    - contributors/你的帳號/001-xxx.md （經驗文章）

# 4. Push 並發 PR
git add contributors/你的帳號/
git commit -m "feat: add lessons from 你的帳號"
git push origin main
# 到 GitHub 網頁發 Pull Request
```

---

## 方式三：開 Issue（最低門檻）
{: .text-yellow-300 }

**適合**：完全不想碰 Git 的人

1. 到 [Issues 頁面](https://github.com/hansai-art/claude-max-club-school/issues/new/choose)
2. 選 **分享新經驗**
3. 填寫表單
4. 維護者會幫你建檔案並 merge

---

## 寫作建議

- **越具體越好**：不要寫「Claude 有時候會出錯」，寫「Claude 在修改 CSS 時會盲目試錯而不是先診斷」
- **附上解決方案**：每篇都要有「可複用的 CLAUDE.md 規則」，這是最有價值的部分
- **一篇一個主題**：不要把 10 個經驗塞在同一篇，拆開來方便別人搜尋
- **用你的話寫**：不需要很正式，口語化反而更好懂
