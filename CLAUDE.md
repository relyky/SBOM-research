# SBOM 研究 LLM Wiki — Schema

> 本檔是此知識庫的「規則書」。任何 LLM agent（Claude Code / Cowork / Codex 等）在操作本資料夾前**必須先讀本檔**。
> 架構依據 Andrej Karpathy 的 LLM Wiki 模式：https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f

## 1. 研究目的

研究 SBOM（Software Bill of Materials，軟體物料清單）在業界的應用與實際操作流程，包含：

- 標準與格式（SPDX、CycloneDX、SWID 等）及其差異
- 法規與政策驅動（美國 EO 14028、NTIA 最低要素、CISA 指引、歐盟 CRA、FDA 醫材要求、台灣相關規範等）
- 產生、驗證、簽章、交換、儲存與消費 SBOM 的工具鏈
- 與漏洞管理的整合（VEX、CVE/OSV、CSAF）
- 企業導入流程（CI/CD 整合、供應商管理、組織角色）與實務案例
- 對自身環境（Python、.NET/C#、React/TypeScript、SQL Server）的落地方式

## 2. 三層架構

| 層 | 位置 | 擁有者 | 規則 |
|---|---|---|---|
| 原始資料 Raw sources | `raw/` | 人類 | **不可修改**。LLM 只讀。是唯一事實來源。 |
| 知識庫 Wiki | `wiki/` | LLM | LLM 全權撰寫與維護；人類閱讀、提問、審核。 |
| 規則 Schema | `CLAUDE.md`（本檔） | 人類 + LLM 共同演進 | 結構、慣例、工作流程的定義。 |

`templates/` 存放各類頁面範本；`README.md` 是給人看的使用說明。

## 3. 目錄結構

```
raw/
  standards/     規格書、標準文件（SPDX spec、CycloneDX spec…）
  regulations/   法規、政策、政府指引
  tools/         工具文件、README、比較文章
  industry/      業界報告、部落格、案例研究、簡報
  papers/        學術論文
  assets/        圖片附件（剪藏工具下載的圖片）
wiki/
  index.md       內容目錄（每次 ingest 都要更新）
  log.md         時序紀錄（只能 append）
  overview.md    研究總覽與目前的整體論點
  concepts/      概念（SBOM、VEX、元件識別 PURL/CPE、依賴深度…）
  standards/     標準/格式（spdx、cyclonedx、swid…）
  tools/         工具（syft、trivy、cdxgen、dependency-track…）
  regulations/   法規與政策
  organizations/ 組織（CISA、NTIA、Linux Foundation、OWASP…）
  practices/     實務流程、導入方法、檢核清單
  sources/       每份原始資料一頁摘要
  analyses/      查詢產出的比較表、分析、結論（從 Query 回存）；簡報原始檔（`.marp.md`）也放這裡
outputs/         匯出成品（簡報 pptx、pdf、圖表等）；非來源、非 wiki 頁，不 ingest、不 lint
```

## 4. 頁面慣例

### 4.1 檔名
- 全小寫英文 kebab-case：`cyclonedx.md`、`ntia-minimum-elements.md`、`eu-cra.md`。
- 來源摘要：`sources/YYYY-MM-DD-<短名>.md`（日期為 ingest 日）。
- 分析：`analyses/<主題>.md`；簡報原始檔 `analyses/<主題>.marp.md`，匯出成品放 `outputs/`（同主檔名）。

### 4.2 Frontmatter（每頁必填，供 Obsidian Dataview 查詢）
```yaml
---
title: 頁面標題
type: concept | standard | tool | regulation | organization | practice | source | analysis | overview
tags: [sbom, ...]
aliases: [其他名稱]
sources: [raw/... 路徑清單]        # 本頁論述依據的原始資料
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: stub | draft | stable
---
```

### 4.3 內文
- 使用**繁體中文（zh-TW）**撰寫；專有名詞首次出現附英文原文，如「物料清單（Bill of Materials, BOM）」。
- 頁面之間用 Obsidian wikilink：`[[cyclonedx]]`、`[[vex|VEX]]`。
- 每個事實性陳述要能追溯來源：句末標註 `[^src]` 腳註，指向 `[[sources/...]]` 或 `raw/` 路徑。
- 未經來源驗證的背景知識需標示 `（待驗證）`。
- 版本、日期敏感的資訊（規格版本、法規生效日、工具版本）要寫明「截至 YYYY-MM」。
- 各類型頁面依 `templates/` 的固定章節撰寫，不要自創結構。

### 4.4 矛盾處理
- 新來源與既有內容衝突時，**在寫入當下處理**：於該頁加入 `> [!warning] 矛盾` callout，列出雙方說法與來源，不要直接覆蓋舊說法。
- 若新資訊取代舊資訊（例如規格改版），保留舊內容於「歷史沿革」段並註明時間。

## 5. 工作流程

### 5.1 Ingest（攝入新來源）
觸發語：「ingest <檔案>」、「處理 raw/ 的新檔案」。
1. 讀取 `raw/` 中的來源（圖片另行查看）。
2. 與使用者簡短討論重點（使用者若說「直接處理」則略過）。
3. 在 `wiki/sources/` 建立摘要頁（依 `templates/source.md`）。
4. 更新或建立相關的 concept / standard / tool / regulation / organization / practice 頁（一份來源常牽動 5–15 頁）。
5. 檢查並標示與既有內容的矛盾。
6. 若影響整體論點，更新 `wiki/overview.md`。
7. 更新 `wiki/index.md`。
8. 在 `wiki/log.md` 末尾 append 一筆紀錄。

如何判斷「尚未 ingest 的來源」：比對 `raw/` 檔案清單與所有 wiki 頁 frontmatter 的 `sources` 欄位，未被引用者即為待處理。

### 5.2 Query（查詢）
1. 先讀 `wiki/index.md` 找到相關頁面，再讀頁面內容。
2. 綜合回答並附上 wikilink 引用。
3. 若答案具保留價值（比較表、分析、決策建議），存成 `wiki/analyses/` 新頁，並更新 index 與 log。
4. 若 wiki 內容不足，明確指出缺口並建議應補充的來源。

### 5.3 Lint（健康檢查）
觸發語：「lint wiki」。檢查並回報（經使用者同意後修正）：
- 頁面間互相矛盾的陳述
- 已被新來源取代的過時說法、標示「截至」日期已久的資訊
- 孤兒頁（沒有任何頁面連入）
- 被提及但尚無專頁的重要概念
- 缺少的交叉引用、frontmatter 欄位不全
- 沒有來源支撐的陳述
- 建議下一步研究問題與值得尋找的新來源
每一項發現必須附上原文引句佐證；無法引證的發現不要回報。

## 6. index.md 與 log.md 格式

### index.md
依類別分節，每頁一行：
`- [[standards/cyclonedx|CycloneDX]] — OWASP 主導的 SBOM 格式，支援 VEX/SaaSBOM（來源 3 份，stable）`

### log.md
只能 append，每筆以固定前綴開頭，方便 `grep "^## \[" wiki/log.md | tail -5` 解析：
```
## [YYYY-MM-DD] ingest | 來源標題
- 新增：[[...]]、[[...]]
- 更新：[[...]]
- 備註：發現與 [[...]] 的矛盾
```
類型：`setup` | `ingest` | `query` | `lint` | `schema`（修改本檔時）。

## 7. 其他規則
- 不刪除 `raw/` 任何檔案；wiki 頁面需刪除或合併時，先徵求使用者同意並記錄於 log。
- 修改本 schema 時，於 log 記錄 `schema` 類型條目。
- 若此資料夾為 git repo，建議每次 ingest/lint 後 commit：`wiki: ingest <來源>`。
