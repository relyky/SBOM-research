---
title: CycloneDX
type: standard
tags: [sbom, standard]
aliases: [CDX]
sources: [raw/tools/clonedx-dotnet.md, raw/tools/syft-grype.sample.md, raw/assets/publish.sbom.cdx.json, raw/tools/SBOM Generation.md, raw/tools/RetireJS - repo.md, raw/industry/軟體物料清單SBOM發展趨勢.md, raw/industry/What Is VEX(Vulnerability Exploitability eXchange).md, raw/industry/軟體供應鏈 - 維基百科，自由的百科全書.md, raw/industry/Best Practices for Naming and Directory Conventions for SBOMs (Software Bill of Materials) in Open Source Projects.md]
current_version: 至少 1.7（2026-10 實測 syft 1.52.0 產出的 `specVersion`；是否為最新版待一手規格）
maintainer: OWASP（依中文維基與資策會 2024-02 文章）
created: 2026-10-01
updated: 2026-10-05
status: stub
---

# CycloneDX

> stub：僅有二手來源與實測輸出；規格說明（`raw/standards/`）尚未取得，BOM 類型與生態系工具待補。

## 概述
OWASP 提出的 SBOM 格式，建立之初即專為 SBOM 設計。[^s4][^m]

## 維護組織與治理
由 OWASP 建構。[^m] 截至資策會 2024-02 文章，尚未取得 ISO 認證，但為 NTIA 認可並推薦的格式之一。[^m]（時效資訊：此後是否取得其他標準組織認證，待一手來源；本庫原骨架曾列別名 ECMA-424，無來源，已移除，待驗證。）

## 版本沿革
| 版本 | 發布日期 | 主要變更 |
|---|---|---|
| 1.4 | 待補 | Aqua 文章的 VEX 範例使用此版本（`specVersion: 1.4`）[^a] |
| 1.6 | 待補 | Retire.js 可輸出（`cyclonedxJSON1_6`）[^rj] |
| 1.7 | 待補 | 2026-10 實測 syft 1.52.0 輸出此版本[^p]；Retire.js 亦可輸出[^rj]；cyclonedx-dotnet 預設輸出 1.7，可選 1.0–1.7[^cd] |

## 資料模型與核心欄位
- JSON 以 `components[]` 列出元件（對照 SPDX 為 `packages[]`）。[^sg]
- 實測檔含 `metadata.component`（被描述的主體）、`metadata.tools`、各元件的 `purl`、`cpe` 與 `properties`。[^p]
- 支援 VEX：以 `vulnerabilities[].analysis` 描述可利用性，見 [[concepts/vex]]。[^a]
- 支援的 BOM 類型（SaaSBOM、HBOM、ML-BOM 等）：待補。

## 支援的序列化格式
JSON（`.cdx.json`）、XML（`.cdx.xml`），檔名慣例見 [[practices/sbom-file-naming]]。[^s1]

## 與其他標準的比較
- 與 [[standards/spdx|SPDX]] 同被 Anchore 稱為「兩種主要產業標準」。[^sg]
- 中文維基與資策會另列 [[standards/swid|SWID]] 為第三種格式。[^s4][^m]

## 工具生態系
- Syft 的主要輸出格式之一，見 [[tools/syft-grype]]。[^sg]
- [[tools/trivy|Trivy]] 可輸出 CycloneDX 並套用 CycloneDX VEX。[^a]
- [[tools/retire-js|Retire.js]] 可輸出 CycloneDX 1.4 XML 與 JSON 1.4／1.6／1.7，1.6、1.7 另有含 `vulnerabilities` 的 `_VEX` 變體。[^rj]
- [[tools/cyclonedx-dotnet|CycloneDX for .NET]]：CycloneDX 官方 GitHub 組織的 .NET 專案 BOM 產生工具，輸出 1.0–1.7，預設 1.7。[^cd]
- 其他語言生態系外掛：待補。

## 採用狀況
資策會文章稱其為 NTIA 官方認可並推薦的格式之一（待對照 NTIA 原文）。[^m]

## 參考來源
[^p]: [[sources/2026-10-01-syft-grype-dotnet-sample]]
[^sg]: [[sources/2026-10-01-anchore-sbom-generation-guide]]
[^a]: [[sources/2026-10-01-aqua-what-is-vex]]
[^m]: [[sources/2026-10-01-moea-sbom-trends]]
[^rj]: [[sources/2026-10-02-retirejs-repo]]
[^cd]: [[sources/2026-10-05-cyclonedx-dotnet-readme]]
[^s1]: [[sources/2026-10-01-openssf-sbom-naming]]
[^s4]: [[sources/2026-10-01-wikipedia-zh-software-supply-chain]]
