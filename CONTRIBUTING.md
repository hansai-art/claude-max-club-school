# 貢獻指南

歡迎來到 Claude MAX 俱樂部學校！這份指南會幫你完成第一次貢獻。

## 貢獻方式

### 方式一：GitHub 網頁版（推薦新手）

完全不需要安裝任何東西，在瀏覽器上就能完成。

1. **Fork**：點右上角的 Fork 按鈕
2. **建資料夾**：進入 `contributors/`，點 `Add file` → `Create new file`，檔名輸入 `你的帳號/index.md`
3. **寫個人簡介**：參考 `contributors/_template/index.md` 的格式
4. **寫經驗文章**：在你的資料夾裡再建一個 `001-描述.md`
5. **發 PR**：回到 repo 首頁，點 `Contribute` → `Open pull request`

### 方式二：本機操作

```bash
git clone https://github.com/你的帳號/claude-max-club-school.git
cd claude-max-club-school
cp -r contributors/_template contributors/你的帳號
# 編輯檔案後
git add contributors/你的帳號/
git commit -m "feat: add lessons from 你的帳號"
git push origin main
```

### 方式三：開 Issue

到 Issues 頁面，選「分享新經驗」，填寫表單即可。

## 文章格式

每篇文章需要：

1. **frontmatter**：`title`、`parent`（你的帳號）、`grand_parent`（貢獻者）
2. **問題**：Claude 犯了什麼錯
3. **原因**：為什麼會這樣
4. **解決方案**：你怎麼解決的
5. **可複用的 CLAUDE.md 規則**：最重要的部分！

## 注意事項

- 一篇一個主題，不要混在一起
- 越具體越好，附上真實案例
- 檔名格式：`001-簡短描述.md`
- 不要修改別人資料夾裡的檔案
- 歡迎修正錯字、補充資訊（透過 PR）
