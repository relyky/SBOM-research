---
title: OpenSSF：開源專案 SBOM 命名與目錄慣例最佳實務
type: source
tags: [sbom, openssf, naming]
sources: [raw/industry/Best Practices for Naming and Directory Conventions for SBOMs (Software Bill of Materials) in Open Source Projects.md]
source_url: https://sbom-catalog.openssf.org/sbom-naming.html
source_author: OpenSSF SBOM Catalog（作者欄未標示）
source_date: 未標示
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# OpenSSF：開源專案 SBOM 命名與目錄慣例最佳實務

## 基本資訊
- 類型：業界指引（社群文件）
- 作者/發布者：[[organizations/openssf|OpenSSF]] SBOM Catalog 網站；作者與發布日期未標示
- 發布日期：未標示
- 可信度評估：業界權威（社群共識文件，非標準）

## 重點摘要
1. 範圍僅限 Source 與 Build 類型 SBOM，對象是直接散布製品（tgz、rpm、deb、zip）的開源專案，不含 Maven/NPM 等生態系自有的中繼資料機制。
2. 發布檔為扁平清單，不使用目錄結構；SBOM 檔名 = 製品檔名 + 對應副檔名（沿用 SLSA provenance 的做法）。
3. 副檔名慣例：CycloneDX 用 `.cdx.json` / `.cdx.xml`；SPDX 用 `.spdx`、`.spdx.json`、`.spdx.xml`、`.spdx.yml`、`.spdx.rdf`。
4. JSON 為必備格式；若同時提供其他格式，仍應提供 JSON，因工具支援度較佳。

## 關鍵主張與數據
- 「The JSON format files should be considered a mandatory requirement and are always available.」— 意涵：交換 SBOM 時以 JSON 為最大公約數。
- 範例：`artifact-1.0.0.tar.gz` → `artifact-1.0.0.tar.gz.cdx.json`。

## 影響的 wiki 頁面
- [[practices/sbom-file-naming]] — 新建
- [[concepts/sbom-types]] — 新建（引用 Source/Build 範圍界定）
- [[standards/cyclonedx]]、[[standards/spdx]] — 補充檔案副檔名慣例
- [[organizations/openssf]] — 新建

## 與既有知識的關係
- 支持：[[sources/2026-10-01-openssf-sbom-types]] 的 SBOM 類型分類（本文引用之）
- 矛盾：無
- 新增：SBOM 檔名與副檔名的具體慣例

## 待追問題
- 非 OpenSSF 的企業內部 SBOM 儲存與命名慣例？
- 此慣例是否被主流工具（Syft、Trivy、cdxgen）預設採用？
