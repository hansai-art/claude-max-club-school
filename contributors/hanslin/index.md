---
layout: default
title: hanslin
parent: 貢獻者
has_children: true
---

# Hans Lin

## 關於我

- **身份**：獨立開發者 / 技術內容創作者
- **工作內容**：經營科技翰林院（techhanlin.tw）技術部落格、開發 iPAS 備考工具
- **技術棧**：WordPress、Lovable + Supabase、Astro、React + TypeScript
- **用 Claude Code 做什麼**：WordPress 文章撰寫與管理、全端開發、自動化腳本（Zoom 排程、部署流程）、SEO 優化
- **使用的 Claude 方案**：Claude MAX
- **用了多久**：超過 10 個月，日均使用

## 我的經驗文章

### 工具使用與效率
- [用 Edit 不要用 Write]({{ site.baseurl }}{% link contributors/hanslin/001-edit-not-write.md %})：Claude 會重寫整個檔案而不是只改 diff
- [平行呼叫工具省 token]({{ site.baseurl }}{% link contributors/hanslin/009-parallel-tool-calls.md %})：能同時做的不要分開做
- [只讀你需要的部分]({{ site.baseurl }}{% link contributors/hanslin/010-read-only-what-you-need.md %})：用 offset/limit 精準讀取
- [不要叫使用者手動執行 SQL]({{ site.baseurl }}{% link contributors/hanslin/008-no-manual-sql.md %})：自己找替代方案

### 診斷與驗證
- [先診斷再動手]({{ site.baseurl }}{% link contributors/hanslin/002-diagnose-first.md %})：不要讓 Claude 猜答案，先跑診斷
- [修完要自己驗證才能說完成]({{ site.baseurl }}{% link contributors/hanslin/004-verify-before-done.md %})：不要樂觀回報「完成」
- [發布前必須 API 回讀驗證]({{ site.baseurl }}{% link contributors/hanslin/007-publish-verify-checklist.md %})：不要憑記憶認為已設定
- [自動化腳本失敗要當場記錄]({{ site.baseurl }}{% link contributors/hanslin/003-automation-debug.md %})：盲目重試不如第一次就記 log

### 覆蓋與版本
- [不要用本地舊檔覆蓋遠端內容]({{ site.baseurl }}{% link contributors/hanslin/005-no-overwrite-remote.md %})：先拉最新版再改
- [每次更新都要遞增版本號]({{ site.baseurl }}{% link contributors/hanslin/006-version-increment.md %})：不要覆蓋舊版檔案

### CSS 與前端（血淚教訓）
- [CSS 改了不檢查就說修好了]({{ site.baseurl }}{% link contributors/hanslin/011-css-no-report-without-verify.md %})：不能只看原始碼就回報
- [inline code 和 code block 的 CSS 會互相干擾]({{ site.baseurl }}{% link contributors/hanslin/012-inline-vs-block-code.md %})：共用 class 要分開處理
- [background-color 蓋不掉 gradient]({{ site.baseurl }}{% link contributors/hanslin/013-gradient-override.md %})：must 加 background-image: none
- [Jekyll link 不會自動加 baseurl]({{ site.baseurl }}{% link contributors/hanslin/014-jekyll-baseurl.md %})：Jekyll 3.10 的坑
- [改 CSS 沒檢查對比度]({{ site.baseurl }}{% link contributors/hanslin/015-contrast-check.md %})：白底黑字、黑底白字，沒有例外
- [圓角在深色模式露出白邊]({{ site.baseurl }}{% link contributors/hanslin/016-border-radius-leak.md %})：直接不用圓角
- [jekyll-build-pages 不編譯本地 _sass]({{ site.baseurl }}{% link contributors/hanslin/017-scss-import-fail.md %})：CSS 放 head_custom.html
- [CSS 疊 patch 不診斷根因]({{ site.baseurl }}{% link contributors/hanslin/018-css-patch-stacking.md %})：改兩次沒修好就 STOP 重診斷

### 規則遵守與專案管理
- [明確禁止的符號還是一直用]({{ site.baseurl }}{% link contributors/hanslin/019-em-dash-habit.md %})：CLAUDE.md 的 NEVER 是硬規則
- [同樣內容寫了三份]({{ site.baseurl }}{% link contributors/hanslin/020-dry-violation.md %})：任何內容只能有一個 canonical 來源
- [用了不存在的 include 檔名]({{ site.baseurl }}{% link contributors/hanslin/021-wrong-include-name.md %})：先查文件再用
- [給 fixed 元素留 padding]({{ site.baseurl }}{% link contributors/hanslin/022-fixed-element-padding.md %})：fixed 不佔文檔流空間
- [內容專案用了程式碼授權]({{ site.baseurl }}{% link contributors/hanslin/023-wrong-license.md %})：內容用 CC BY-SA，不是 MIT
- [基本配置檔都忘了建]({{ site.baseurl }}{% link contributors/hanslin/024-missing-gitignore.md %})：.gitignore 和版本固定是第一步
- [不了解平台限制就加設定]({{ site.baseurl }}{% link contributors/hanslin/025-permalink-pretty-fail.md %})：先確認版本再動手
