---
layout: default
title: "vercel env add 用 echo 會把換行字元存進去"
parent: fishtvlvoe
grand_parent: 貢獻者
date: 2026-05-11
still_relevant: true
permalink: /contributors/fishtvlvoe/009-vercel-env-echo-newline/
---

# `vercel env add` 用 echo 會把換行字元存進去

## 問題

用 `echo "value" | vercel env add KEY production` 設定環境變數，之後呼叫相關 API 一直回 4xx，但 Vercel 沒有任何 alert，`.catch()` 也吞掉錯誤，表面上完全正常。

真實案例一：設定 `LINE_LOGIN_CHANNEL_ID`，LINE OAuth 一直回「invalid client_id」，但 ID 明明正確。實際原因：ID 後面多了一個 `\n`，變成 `1234567890\n`，被 LINE 拒絕。

真實案例二：設定 `TOSEND_FROM_EMAIL`，忘記密碼信永遠寄不出去，Vercel Function logs 沒有任何 error。原因：email 變成 `fish@example.com\n`，SMTP API 回 4xx，但被 `.catch()` 吞掉。

## 原因

`echo` 指令預設會在輸出結尾加一個換行字元（`\n`）。用 pipe 傳給 `vercel env add` 時，這個 `\n` 也被一起存進去，成為 secret 值的一部分。大多數 API 不接受帶 `\n` 的值，但錯誤通常被吞掉，很難發現。

## 解決方案

**改用 `printf`（不加換行）**：

```bash
# 錯誤（會多一個 \n）
echo "my-secret-value" | vercel env add MY_KEY production

# 正確（printf 不加換行）
printf "my-secret-value" | vercel env add MY_KEY production

# 或存到暫存檔
printf "my-secret-value" > /tmp/v && vercel env add MY_KEY production < /tmp/v
```

**加完之後 MUST 驗證**：

```bash
# pull 下來確認值結尾沒有 \n
vercel env pull /tmp/.env.prod --environment=production
grep "^MY_KEY=" /tmp/.env.prod | cat -A  # $ 符號前不應該有 ^M 或多餘字元
```

## 可複用的 CLAUDE.md 規則

```markdown
### vercel env add
- 禁止用 echo "value" | vercel env add KEY production
- echo 會帶 \n 進去，API 收到 "value\n" 回 4xx → 被 catch 吞掉 → 靜默失敗
- 正確做法：printf "value" | vercel env add KEY production
- 每次加完 MUST 驗證：vercel env pull /tmp/.env.prod && grep "^KEY=" /tmp/.env.prod
- 值結尾應該是 "value"，不是 "value\n"
```
