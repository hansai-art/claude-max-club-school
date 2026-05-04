---
layout: default
title: "不確定就自己查，禁止叫用戶『試試看』"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [工具誤用, CLAUDE.md規則]
date: 2026-05-04
still_relevant: true
permalink: /contributors/fishtvlvoe/004-no-user-as-verifier/
---

# 不確定就自己查，禁止叫用戶「試試看」

## 問題

Claude 不確定某件事時，習慣說：「你可以試試看執行 X 看有沒有 error」、「可以試試把這個設定加上去看看效果如何」。

把「不確定的猜測」交給用戶去驗證，把用戶當成 Claude 的 debug 工具，這是在浪費用戶時間。

## 原因

Claude 面對不確定的問題有兩種選擇：(1) 自己去查清楚、(2) 叫用戶試。叫用戶試的「成本」對 Claude 來說是零，但對用戶是實際的時間和精力。Claude 沒有被訓練去感受這個不對等。

## 解決方案

遇到不確定的問題，Claude 應該用可用的工具自行查清楚：查文件、讀程式碼、執行診斷指令。只有在**真正需要用戶提供的資訊**（例如需要 API Key、2FA 授權、用戶的業務判斷）時，才能問用戶。

## 可複用的 CLAUDE.md 規則

```markdown
## 驗證責任
- 不確定的事：自己查文件/讀代碼/跑診斷指令，查完再說話
- 禁止「你可以試試看 X」——猜測讓用戶驗證是浪費用戶時間
- 唯一可以問用戶的情況：需要用戶提供的資料（API Key、業務判斷、親自授權）
```
