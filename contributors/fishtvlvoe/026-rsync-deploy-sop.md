---
layout: default
title: "rsync 部署完整 SOP：連線測試、部署、chmod 修正權限"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [部署, CLAUDE.md規則]
date: 2026-04-01
still_relevant: true
permalink: /contributors/fishtvlvoe/026-rsync-deploy-sop/
---

# rsync 部署完整 SOP：連線測試、部署、chmod 修正權限

## 問題

用 rsync 部署後，靜態資源（CSS/JS/圖片）回 403 Forbidden。代碼部署成功，但網站壞了。

另一個常見問題：rsync 部署後沒有修正目錄/檔案權限，WordPress 或 Apache 讀不到檔案。

## 原因

rsync 預設**保留 source 端的權限**。如果 source 目錄（例如 macOS 本地）的目錄預設是 700，rsync 會把 700 帶過去，Apache/Nginx 沒有讀取權限，就會回 403。

這個問題的坑在於：每次 rsync 部署都可能遇到，不只是第一次——只要 source 端建立了新目錄，就可能有新的 700 目錄被帶過去。

## 解決方案

完整的 sshpass + rsync 部署 SOP：

**Step 1：測試 SSH 連線**
```bash
SSHPASS='<password>' sshpass -e ssh \
  -o StrictHostKeyChecking=no \
  -p <port> user@host \
  'echo "連線成功"'
```

**Step 2：執行 rsync 部署**
```bash
SSHPASS='<password>' rsync -avz \
  -e "sshpass -e ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -p <port>" \
  ./local-dir/ \
  user@host:/remote/path/
```

**Step 3：部署後強制修正權限（每次都要做）**
```bash
SSHPASS='<password>' sshpass -e ssh \
  -o StrictHostKeyChecking=no \
  -p <port> user@host \
  'find /remote/path -type d -exec chmod 755 {} \; && find /remote/path -type f -exec chmod 644 {} \;'
```

不管 source 端權限長怎樣，Step 3 都強制重設，確保 Apache/Nginx 可以讀取。

**診斷：** 如果看到 403，先 SSH 確認目錄權限是否為 700：`ls -la /remote/path/`

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- rsync 部署後 MUST 執行：
  find <plugin_dir> -type d -exec chmod 755 {} \;
  find <plugin_dir> -type f -exec chmod 644 {} \;
  每次部署都強制重設，不管 source 端權限，否則靜態資源會 403。
- sshpass 連線測試：SSHPASS='<pw>' sshpass -e ssh -o StrictHostKeyChecking=no -p <port> user@host
```
