---
layout: default
title: 開始貢獻
nav_order: 2
---

# 開始貢獻
{: .fs-8 }

讓你的 Claude 幫你貢獻，一句話搞定。
{: .fs-5 .fw-300 }

---

## 推薦方式：讓你的 AI 幫你做
{: .text-green-300 }

你都有 Claude MAX 了，為什麼還要自己手動操作 Git？

**直接把下面這段話貼給你的 Claude Code：**

````
幫我貢獻一篇經驗到 claude-max-club-school：

1. fork https://github.com/hansai-art/claude-max-club-school
2. 在 contributors/ 下建立我的資料夾（用我的 GitHub username）
3. 參考 contributors/_template/ 的格式，建立 index.md（個人簡介）和一篇經驗文章
4. 經驗主題：（這裡填你想分享的踩坑經驗）
5. push 後幫我發 PR
````

**就這樣。** 你的 Claude 會自動 fork、建資料夾、寫文章、發 PR。你只需要：
1. 告訴它你踩過什麼坑
2. Review 它幫你寫的內容
3. 確認發 PR

---

## 經驗文章長什麼樣？

每篇文章只需要四個區塊：

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

你不需要記住這個格式。你的 Claude 會自動參考 `_template/` 裡的範本。

---

## 其他方式

如果你比較習慣手動操作，也可以：

### GitHub 網頁版

1. 到 [Repo 頁面](https://github.com/hansai-art/claude-max-club-school) 點 **Fork**
2. 在 `contributors/` 下建立 `你的帳號/index.md`
3. 寫文章，發 PR

### 本機 Git

```bash
git clone https://github.com/你的帳號/claude-max-club-school.git
cd claude-max-club-school
cp -r contributors/_template contributors/你的帳號
# 編輯檔案後
git add contributors/你的帳號/
git commit -m "feat: add lessons from 你的帳號"
git push origin main
# 到 GitHub 發 PR
```

---

## 寫作建議

- **越具體越好**：不要寫「Claude 有時候會出錯」，寫「Claude 在修改 CSS 時會盲目試錯而不是先診斷」
- **附上解決方案**：每篇都要有「可複用的 CLAUDE.md 規則」，這是最有價值的部分
- **一篇一個主題**：不要把 10 個經驗塞在同一篇，拆開來方便別人搜尋
- **用你的話寫**：不需要很正式，口語化反而更好懂
