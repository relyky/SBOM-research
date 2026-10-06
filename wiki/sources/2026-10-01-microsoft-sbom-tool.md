---
title: microsoft/sbom-tool README
type: source
tags: [sbom, tool, spdx, microsoft, dotnet]
sources: [raw/tools/Microsoft sbom-tool.md]
source_url: https://github.com/microsoft/sbom-tool
source_author: Microsoft
source_date: 未標示（剪藏於 2026-10-01）
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# microsoft/sbom-tool README

## 基本資訊
- 類型：工具文件（官方 README）
- 作者/發布者：Microsoft
- 發布日期：未標示
- 可信度評估：官方一手

## 重點摘要
1. 定位：可擴充、企業級的 SBOM 產生工具，輸出 SPDX 2.2 與 SPDX 3.0；以 Component Detection 函式庫偵測元件，以 ClearlyDefined API 補授權資訊。
2. 提供三種功能：`generate`（產生）、`validate`（驗證）、`redact`（移除 SBOM 中的檔案參照，目前僅支援 SPDX 2.2）。
3. 安裝：`winget install Microsoft.SbomTool`、`brew install sbom-tool`、手動下載執行檔（Windows／Linux／macOS）、自建 Docker 映像、`dotnet tool install --global Microsoft.Sbom.DotNetTool`；另有 `Microsoft.Sbom.Api` NuGet 套件可在 C# 程式中呼叫。
4. 產生命令：`sbom-tool generate -b <drop path> -bc <build components path> -pn <name> -pv <version> -ps <supplier> -nsb <namespace uri base>`。`-b` 資料夾內所有出貨檔案會被雜湊並列入 files 區段；`-bc` 通常是原始碼資料夾，工具掃描 `*.csproj`、`package.json` 等專案檔判斷建置所用元件。
5. 預設 SPDX 2.2，加 `-mi SPDX:3.0` 產生 SPDX 3.0。每份 SBOM 有唯一 namespace：`<nsb>/<packageName>/<packageVersion>/<new-guid>`。
6. 驗證預設讀取 `<drop path>\_manifest\spdx_2.2\manifest.spdx.json`（3.0 為 `spdx_3.0`）。
7. 提供 GitHub Actions 與 Azure DevOps Pipelines 的整合指南；遙測只輸出到本機輸出路徑，不送往 Microsoft。
8. 專案因 SBOM 的敏感、法規性質不接受外部貢獻，外部使用者可 fork 自行維護。

## 關鍵主張與數據
- 「The tool uses the Component Detection libraries to detect components and the ClearlyDefined API to populate license information」— 意涵：元件偵測與授權補全分屬兩個外部元件。
- 「No data is submitted to Microsoft.」— 意涵：遙測僅落地於本機。

## 影響的 wiki 頁面
- [[tools/microsoft-sbom-tool]] — 新建
- [[standards/spdx]] — 補充 SPDX 2.2／3.0 版本線索與 namespace 概念
- [[practices/sbom-file-naming]] — 補充此工具預設輸出路徑與命名慣例不同
- [[practices/dotnet-sbom-syft-grype]] — 補充替代方案
- [[overview]]、[[index]]

## 與既有知識的關係
- 支持：[[sources/2026-10-01-moea-sbom-trends]] 稱「微軟提供 SBOM 檢測工具，以 SPDX 格式」。
- 矛盾（來源內部）：frontmatter 標題稱「create SPDX 2.2 compatible SBOMs」，內文稱「SPDX 2.2 and SPDX 3.0」。內文與命令範例較完整，採後者；標題疑為較舊的 repo 描述（待驗證）。
- 新增：SPDX 3.0 已被主流工具支援；validate／redact 功能；以 `.csproj` 判斷元件的做法。

## 待追問題
- Component Detection 與 ClearlyDefined 的能力與限制（尚無來源）。
- 同一 .NET 專案分別用 sbom-tool 與 syft 產出的元件清單是否一致？
