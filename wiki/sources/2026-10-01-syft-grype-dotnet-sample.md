---
title: 實測紀錄：用 syft + grype 為 .NET 專案產生 SBOM 並掃描漏洞
type: source
tags: [sbom, tool, syft, grype, dotnet, hands-on]
sources: [raw/tools/syft-grype.sample.md, raw/assets/publish.sbom.cdx.json, raw/assets/publish.grype.json]
source_url: 無（使用者自行實測紀錄）
source_author: 使用者（Rely）
source_date: 2026-10-01
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# 實測紀錄：syft + grype 掃描 .NET 專案

## 基本資訊
- 類型：實測紀錄（第一手經驗，非公開來源）
- 作者/發布者：使用者；對象為內部 .NET 專案 AsvtQUO
- 發布日期：2026-10-01
- 可信度評估：第一手實測；結論僅適用於該專案與當時版本（syft 1.52.0、grype 0.119.0，Windows 11 + Git Bash）

## 重點摘要
1. 用 winget 安裝 syft 與 grype；`syft dir:. -o cyclonedx-json=sbom.cdx.json`。
2. 掃整個專案目錄會連 `bin/`、`obj/`、`publish/` 一併掃，元件重複計算，共 1365 個；只掃發佈產物 `syft dir:publish` 則為 176 個，較貼近正式環境。可用 `--exclude` 排除建置產物。
3. 未指定時 syft 警告無名稱與版本；正式交付應加 `--source-name`、`--source-version`（版本取自 `publish/AsvtQUO.deps.json`，如 `1.7.14-release`）。
4. grype 首次自動下載資料庫；`grype db status` 查版本，`grype db update` 手動更新；`grype sbom:publish.sbom.cdx.json -o table`，無漏洞時輸出 `No vulnerabilities found`。
5. 結果（2026-10-01）：兩份 SBOM 的漏洞數皆為 0。
6. 限制：grype 只能比對有 purl 的套件（本例為 NuGet）；無 purl 的元件與 .NET 執行環境本身不在掃描範圍。

## 關鍵主張與數據
- 附檔 `publish.sbom.cdx.json` 實際內容：CycloneDX `specVersion` 1.7，由 syft 1.52.0 產生，`metadata.component` 為 AsvtQUO / 1.7.14-release，共 176 個元件（170 個 `library`、6 個 `application`），170 個皆為 `pkg:nuget` purl。（本庫對該檔的直接檢視）
- 附檔 `publish.grype.json`：`matches` 為空陣列；grype 0.119.0；弱點資料庫 schema v6.1.9，建置於 2026-09-30，資料來源涵蓋 nvd、github、govulndb、epss、kev 及多個 Linux 發行版等。
- 「grype 只能比對有 purl 的套件」— 意涵：0 漏洞不等於無風險，需另行處理無 purl 元件與執行環境。

## 影響的 wiki 頁面
- [[practices/dotnet-sbom-syft-grype]] — 新建
- [[tools/syft-grype]] — 補實測紀錄
- [[standards/cyclonedx]] — 補充 CycloneDX 1.7 已見於實際工具輸出
- [[overview]] — 更新 .NET 落地論點

## 與既有知識的關係
- 支持：官方文件對 `dir:`、`-o cyclonedx-json=`、`grype sbom:` 的用法
- 矛盾：無
- 新增：目錄掃描 vs 發佈產物掃描的元件數差異；purl 覆蓋限制；.NET 實證

## 待追問題
- 無 purl 的 6 個 `application` 元件是什麼？是否需人工補登？
- 0 漏洞是否受限於 NVD／CPE 對 NuGet 套件的匹配精度（見 SBOM 檔內 CPE 欄位）？
- 同一專案改用 Trivy 或 cdxgen（CycloneDX 官方 .NET 工具）結果是否一致？
