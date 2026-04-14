---
layout: default
title: "經驗標題（描述 Claude 犯了什麼錯）"
parent: 你的GitHub帳號
grand_parent: 貢獻者
tags: [常見錯誤]              # 可選：常見錯誤 / Debug心得 / 工作流程 / 提示技巧 / 自動化
date: 2026-01-01              # 發現這個問題的大概日期
still_relevant: true          # 如果 Claude 已經修好這個問題，改成 false
---

# 經驗標題

<!-- 把上面的標題改成你的經驗描述 -->
<!-- 把 frontmatter 裡的 parent 改成你的 GitHub 帳號 -->

## 問題

<!-- Claude 犯了什麼錯？越具體越好 -->
<!-- 例如：Claude 在修改現有檔案時，會用 Write 工具重寫整個檔案，而不是用 Edit 工具只改需要改的部分 -->

## 原因

<!-- 為什麼 Claude 會這樣做？ -->
<!-- 例如：Write 工具的預設行為是覆蓋整個檔案，Claude 如果沒有明確指令，傾向用更「安全」的方式 -->

## 解決方案

<!-- 你怎麼解決的？ -->
<!-- 例如：在 CLAUDE.md 裡明確指定「Prefer Edit over Write for existing files」 -->

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- Prefer Edit over Write for existing files — 只送 diff，不重寫整檔。
```

<!-- 這是最有價值的部分！讓別人可以直接複製貼上 -->
