# 貢獻指南

歡迎來到 Claude MAX 俱樂部學校！這份指南會幫你完成第一次貢獻。

## 貢獻方式

### 推薦：讓你的 Claude Code 幫你做

你都有 Claude MAX 了，直接讓 AI 代勞最快。把下面這段話貼給你的 Claude Code：

```
幫我貢獻經驗到 claude-max-club-school：

1. fork https://github.com/hansai-art/claude-max-club-school
2. 在 contributors/ 下建立我的資料夾（用我的 GitHub username）
3. 參考 contributors/_template/ 的格式，建立 index.md（個人簡介）
4. 讀取我的 ~/.claude/CLAUDE.md 和 memory 裡的 feedback 記錄，把所有踩坑經驗都整理成文章，越多篇越好
5. 每篇文章都要附上「可複用的 CLAUDE.md 規則」
6. push 後幫我發 PR
```

你的 Claude 會自動掃描你的 CLAUDE.md 和 memory，把累積的所有教訓整理成文章。貢獻越多篇越好。

### 手動操作

也可以自己動手：

1. [Fork](https://github.com/hansai-art/claude-max-club-school/fork) 這個 repo
2. 在 `contributors/你的帳號/` 下建立 `index.md` 和經驗文章
3. 參考 `contributors/_template/` 的格式
4. 發 Pull Request

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
