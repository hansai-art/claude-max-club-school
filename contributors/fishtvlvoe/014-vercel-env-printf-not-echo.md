---
layout: default
title: "Vercel env add 禁用 echo，用 printf 避免隱形 \\n"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [DevOps, 診斷不足]
date: 2026-05-04
still_relevant: true
permalink: /contributors/fishtvlvoe/014-vercel-env-printf-not-echo/
---

# Vercel env add 禁用 echo，用 printf 避免隱形 `\n`

## 問題

用 `echo "value" | vercel env add X production` 設定環境變數後，功能神秘失效：

- OAuth 登入失敗（`client_id` 被 API 拒絕）
- 寄信失敗（`from_email` 地址無效）
- 功能看起來有在執行，但就是回 4xx 被吞掉

用 `vercel env pull` 把值拉下來，用十六進位查才發現：值的結尾有一個 `\n`（`fish@example.com\n` 而不是 `fish@example.com`）。

## 原因

`echo` 在輸出時會自動在結尾加上換行符（`\n`）。用 pipe 傳給 `vercel env add` 時，這個換行符被當作值的一部分存進去。

Vercel 存的是 `fish@example.com\n`，程式碼讀出來用這個值去呼叫外部 API 時，API 收到一個帶換行符的字串，當成無效值拒絕。

錯誤通常被 `.catch()` 靜默吞掉，沒有任何 alert 或 error log，只有功能不動。

已踩坑兩次：
1. `LINE_LOGIN_CHANNEL_ID` → LINE OAuth `client_id` 帶 `\n` → LINE 登入失敗
2. `TOSEND_FROM_EMAIL` → 忘記密碼信永遠寄不出去

## 解決方案

用 `printf`（不加換行）替代 `echo`：

```bash
# 錯誤：echo 會加 \n
echo "fish@example.com" | vercel env add TOSEND_FROM_EMAIL production

# 正確：用 printf 不加換行，或用 file 傳入
printf "fish@example.com" > /tmp/v && vercel env add TOSEND_FROM_EMAIL production < /tmp/v
```

**加完必須驗證**：
```bash
vercel env pull /tmp/.env.prod --environment=production
grep "^TOSEND_FROM_EMAIL=" /tmp/.env.prod
# 應該看到 TOSEND_FROM_EMAIL="fish@example.com" 而不是 "fish@example.com\n"
```

## 可複用的 CLAUDE.md 規則

```markdown
## Vercel 環境變數
- 禁止 `echo "value" | vercel env add`——echo 帶換行，存進 Vercel 變成隱形 \n
- 正確做法：`printf "value" > /tmp/v && vercel env add X production < /tmp/v`
- 每次加完 MUST 驗證：`vercel env pull /tmp/.env.prod && grep "^X=" /tmp/.env.prod`
- 隱形 \n 的症狀：OAuth/email 等外部 API 回 4xx，被 .catch() 吞掉，無 error log
```
