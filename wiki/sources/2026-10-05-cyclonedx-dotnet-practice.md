---
title: 實測：cyclonedx-dotnet 安裝與基本使用
type: source
tags: [sbom, tool, cyclonedx, dotnet, practice]
sources: [raw/tools/clonedx-dotnet-practice.md]
source_url: 無（使用者自行記錄）
source_author: 使用者
source_date: 2026-10-05（依 ingest 日；檔內未標日期）
created: 2026-10-05
updated: 2026-10-05
status: draft
---

# 實測：cyclonedx-dotnet 安裝與基本使用

## 基本資訊
- 類型：工具文件（使用者實測筆記）
- 作者/發布者：使用者
- 發布日期：檔內未載明
- 可信度評估：個人觀點／單次實測；僅含指令與簡短輸出，無 SBOM 內容

## 重點摘要
0. 動機：使用者測得 syft 對 .NET 套件拿不到授權資訊，無法快速檢查 license 是否核可；cyclonedx-dotnet 對 .NET 套件支援較完整。
1. 安裝：`dotnet tool install --global CycloneDX`，輸出顯示工具 `cyclonedx` 版本 6.2.0，指令為 `dotnet-CycloneDX`。
2. 最簡用法：`dotnet-CycloneDx QadbGraphQL.slnx -o .sbom`，寫出 `.sbom\bom.xml`；**預設為 XML，預設檔名 `bom.xml`**。
3. 一般用法：`-o .sbom -F Json -t -fn myproject-version-cdx.json`，即指定輸出目錄、JSON 格式、排除測試專案、自訂檔名。
4. 輸入為 `.slnx` 方案檔，驗證 README 所列 `.slnx` 支援。

## 關鍵主張與數據
- 「經測試 syft 工具拿不到 NET 套件的授權資訊，這樣就無法快速檢查 license 是否核可。此工具對 NET 套件支援較完整。」— 意涵：選用 cyclonedx-dotnet 的主因是授權合規。本庫直接檢視 `raw/assets/publish.sbom.cdx.json`（syft 1.52.0 實測輸出），全檔無 "license" 字樣，與此說法相符；但是否因 .NET 特有、或需額外設定，無一手來源，（待驗證）。
- 「已成功安裝工具 'cyclonedx' ('6.2.0' 版)」— 意涵：補上 [[tools/cyclonedx-dotnet]] 的 `version_checked`。
- 「產生 XML 格式的 cdx 檔。存入 `.sbom` 目錄。輸出預設檔名 `bom.xml`。」— 意涵：README 的 `-F` 預設 Auto 加預設檔名「bom.xml 或 bom.json」，實測在此情境落為 XML、`bom.xml`。
- 「產生 JSON 格式的 cdx 檔。存入 `.sbom` 目錄。並指定輸出檔名。」— 意涵：`-F Json` 搭配 `-fn` 可自訂 JSON 檔名。
- 輸出檔名 `myproject-version-cdx.json` 不符 [[practices/sbom-file-naming]] 的 `.cdx.json` 副檔名慣例，若採該慣例應改為 `myproject-version.cdx.json`。（對照為本庫推論）

## 影響的 wiki 頁面
- [[tools/cyclonedx-dotnet]] — 補實測紀錄與版本
- [[practices/dotnet-sbom-syft-grype]] — 替代方案補實測指令
- [[overview]]、[[index]]

## 與既有知識的關係
- 支持：[[sources/2026-10-05-cyclonedx-dotnet-readme]] 的 `-F`、`-t`、`-fn`、`-o` 說明與 `.slnx` 支援。
- 矛盾：無。
- 新增：實測工具版本 6.2.0；預設輸出為 XML；使用動機——syft 對 .NET 套件缺授權資訊。
- 補充：[[tools/syft-grype]] 原未記載授權欄位限制，已補註。

## 待追問題
- cyclonedx-dotnet 產出的授權資訊實際內容（SPDX ID 或名稱、涵蓋率）未附；README 提到 `-egl` 可經 GitHub API 解析授權，是否有啟用未記。
- syft 缺授權是否可由設定或其他掃描來源改善？
- 產出的 BOM 內容（元件數、是否含 purl、規格版本）未附，無法與 syft 的 176 個元件比較。
- 未使用 `-ef`、`-sn`、`-sv`，metadata 預設值（版本 `0.0.0`）實際呈現未知。
- 實測環境（OS、.NET SDK 版本）未記。
