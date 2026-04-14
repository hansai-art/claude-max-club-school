---
layout: default
title: 運作方式
nav_order: 3
---

# 運作方式
{: .fs-8 }

---

## 整體架構

```
claude-max-club-school/
├── contributors/          ← 每人一個資料夾
│   ├── hanslin/
│   │   ├── index.md       ← 個人簡介
│   │   ├── 001-xxx.md     ← 經驗文章
│   │   └── 002-xxx.md
│   ├── johndoe/
│   │   └── ...
│   └── _template/         ← 新人複製這個開始
├── lessons/               ← 按主題分類的索引
├── snippets/              ← 可直接複製的 CLAUDE.md 規則
└── index.md               ← 你現在看到的首頁
```

## 流程

1. **貢獻者** 在自己的資料夾寫 Markdown 文章
2. **發 PR** 給這個 repo
3. **維護者 review** 後 merge
4. **GitHub Pages 自動更新**，文章出現在預覽網站上
5. **任何人** 都可以瀏覽、搜尋、複製 CLAUDE.md 規則到自己的專案

## 為什麼用 GitHub？

- **版本控制**：每次修改都有記錄，不怕搞壞
- **PR Review**：社群互相 review，品質更好
- **GitHub Pages**：免費的預覽網站，自動部署
- **低門檻**：會寫 Markdown 就能貢獻，不需要會程式

## 技術細節

- 靜態網站引擎：[Jekyll](https://jekyllrb.com/)
- 主題：[just-the-docs](https://just-the-docs.com/)
- 託管：GitHub Pages
- 搜尋：內建全站搜尋（just-the-docs 提供）
- 貢獻者只需要寫 Markdown，不需要碰任何程式碼
