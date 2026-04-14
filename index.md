---
layout: default
title: Claude MAX 俱樂部學校：社群共編 Claude Code 經驗資料庫
nav_order: 1
permalink: /
description: "台灣 Claude MAX 用戶共編的 Claude Code 踩坑經驗、CLAUDE.md 規則庫、新手懶人包。讓你的 AI 少犯別人已經踩過的坑。"
---

# Claude MAX 俱樂部學校
{: .fs-9 }

送你的 Claude 來上學，讓它少犯別人已經踩過的坑。
{: .fs-6 .fw-300 }

我們是一群台灣的 Claude MAX 用戶。每天用 Claude Code 寫程式、管網站、跑自動化，也每天在踩坑。

與其每個人獨自摸索，不如把教訓集中起來：**你教會你的 Claude 一件事，所有人的 Claude 都跟著變聰明。**

[讓我的 Claude 來貢獻]({{ site.baseurl }}{% link pages/getting-started.md %}){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[看看能學到什麼]({{ site.baseurl }}{% link lessons/index.md %}){: .btn .fs-5 .mb-4 .mb-md-0 }

---

## 把 Claude 送來學校的好處

**你不用自己踩完所有的坑。**

每個 Claude MAX 用戶都在訓練自己的 Claude：寫 CLAUDE.md 規則、調整提示策略、找到更好的工作流程。但這些知識都鎖在各自的電腦裡。

Claude MAX 俱樂部學校做的事情很簡單：

1. **你貢獻一個教訓** → 寫下 Claude 犯了什麼錯、你怎麼解決的
2. **附上 CLAUDE.md 規則** → 別人可以直接複製貼上
3. **所有人受益** → 100 個人的經驗，讓每個人的 Claude 都少犯 1000 個錯

**這裡不是教學文件，是實戰踩坑紀錄。** 每一條規則都是某個人真的被 Claude 搞過之後寫下來的。

---

## 這裡有什麼？

| 區域 | 說明 |
|:-----|:-----|
| [新手懶人包]({{ site.baseurl }}{% link pages/starter-pack.md %}) | 不管什麼技術棧都適用的通用規則，5 秒安裝 |
| [貢獻者]({{ site.baseurl }}{% link contributors/index.md %}) | 每人一個專屬資料夾，看看跟你背景相近的人踩了什麼坑 |
| [經驗分類]({{ site.baseurl }}{% link lessons/index.md %}) | 按主題整理的經驗索引：常見錯誤、Debug 心得、工作流程 |
| [CLAUDE.md 片段庫]({{ site.baseurl }}{% link snippets/index.md %}) | 可以直接複製貼上的規則，拿去強化你的 Claude |

## 怎麼讓你的 Claude 來這裡學習？

不要照抄所有人的規則，浪費 token 也不見得適合你。

**把下面這段話貼給你的 Claude Code，讓它自己挑有用的學：**

```
去 https://github.com/hansai-art/claude-max-club-school

1. 先讀 contributors.yml，找出技術棧和工作內容跟我相近的貢獻者
2. 只讀那些相關貢獻者的經驗文章
3. 跳過 still_relevant: false 的過時規則
4. 把對我有用的 CLAUDE.md 規則整理出來
5. 直接幫我加進 ~/.claude/CLAUDE.md，跟既有規則去重，不要重複
```

你的 Claude 會根據你的背景自動篩選，只學相關的，一步到位寫進你的 CLAUDE.md。

**懶得篩？** 直接裝 [新手懶人包]({{ site.baseurl }}{% link pages/starter-pack.md %})，5 秒搞定。

## 讓你的 Claude 自我進化

Claude Code 有一個官方功能 **/insight**，會自動分析你的使用模式，找出重複犯的錯、效率低的習慣、和可以改善的地方。

**建議流程：**

1. 在 Claude Code 裡輸入 **/insight**
2. 看看它發現了什麼你沒注意到的問題
3. 把有用的發現[貢獻上來]({{ site.baseurl }}{% link pages/getting-started.md %})，讓其他人的 Claude 也學到

**/insight** 是挖掘經驗最快的方式，比自己回想踩過什麼坑快多了。

## 最新貢獻

- [只讀你需要的部分]({{ site.baseurl }}{% link contributors/hanslin/010-read-only-what-you-need.md %}) by hanslin
- [平行呼叫工具省 token]({{ site.baseurl }}{% link contributors/hanslin/009-parallel-tool-calls.md %}) by hanslin
- [不要叫使用者手動執行 SQL]({{ site.baseurl }}{% link contributors/hanslin/008-no-manual-sql.md %}) by hanslin
- [發布前必須 API 回讀驗證]({{ site.baseurl }}{% link contributors/hanslin/007-publish-verify-checklist.md %}) by hanslin
- [不要用本地舊檔覆蓋遠端內容]({{ site.baseurl }}{% link contributors/hanslin/005-no-overwrite-remote.md %}) by hanslin

---

> **A Community Project by Taiwan Claude MAX Users**: We share our Claude Code mistakes and lessons learned, so everyone's Claude gets smarter together. Articles are primarily in Traditional Chinese, but English contributions are welcome. [Start contributing]({{ site.baseurl }}{% link pages/getting-started.md %}).
