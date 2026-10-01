# SBOM 研究知識庫（LLM Wiki）

依 [Karpathy 的 LLM Wiki 模式](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) 建立：**人類負責蒐集來源與提問，LLM 負責撰寫、交叉引用與維護 wiki。** 知識隨每次閱讀與提問累積，而不是消失在聊天紀錄中。

## 結構
| 位置 | 用途 | 誰編輯 |
|---|---|---|
| `raw/` | 原始資料（PDF、網頁剪藏、規格書） | 你（放入後不再修改） |
| `wiki/` | LLM 撰寫的知識頁 | LLM |
| `CLAUDE.md` | 規則書（結構、慣例、流程） | 你 + LLM |
| `templates/` | 各類頁面範本 | 你 + LLM |

## 日常使用
1. **加入來源**：把文件存進 `raw/` 對應子資料夾（網頁可用 Obsidian Web Clipper 轉成 Markdown，圖片放 `raw/assets/`）。
2. **Ingest**：對 Claude 說「ingest raw/standards/xxx.pdf」或「處理 raw/ 中尚未 ingest 的檔案」。
3. **Query**：直接提問，例如「比較 SPDX 與 CycloneDX 在 VEX 支援上的差異」，有價值的答案請 Claude「存成分析頁」。
4. **Lint**：定期說「lint wiki」，檢查矛盾、過時資訊、孤兒頁與知識缺口。

## 建議工具
- **Obsidian**：把本資料夾當 vault 開啟，即可瀏覽 wikilink、Graph view；搭配 Dataview 外掛可依 frontmatter 查詢（如列出所有 `status: stub` 頁）。
- **Git**：本資料夾已初始化為 git repo，每次 ingest 後 commit，即有完整版本歷史。

## 起點
- [wiki/index.md](wiki/index.md) — 目錄
- [wiki/overview.md](wiki/overview.md) — 研究問題與來源蒐集路線圖
