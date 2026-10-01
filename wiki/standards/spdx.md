---
title: SPDX
type: standard
tags: [sbom, standard]
aliases: [Software Package Data Exchange, ISO/IEC 5962]
sources: [raw/tools/sbom-tool.md, raw/tools/SBOM Generation.md, raw/industry/軟體物料清單SBOM發展趨勢.md, raw/industry/軟體供應鏈 - 維基百科，自由的百科全書.md, raw/industry/Best Practices for Naming and Directory Conventions for SBOMs (Software Bill of Materials) in Open Source Projects.md]
current_version: 未查證（僅知 ISO/IEC 5962:2021；截至 2026-10 的最新規格版本待一手規格）
maintainer: Linux Foundation（依資策會 2024-02 文章，SPDX 為其技術項目之一）
created: 2026-10-01
updated: 2026-10-01
status: stub
---

# SPDX

> stub：僅有二手來源；規格書（`raw/standards/`）尚未取得，資料模型與 profile 待補。

## 概述
軟體包資料交換規範（Software Package Data Exchange）是 ISO/IEC 5962:2021 指定的 SBOM 格式。[^s4] 開放標準中提到自動化 SBOM 流程的需求。[^s4]

## 維護組織與治理
由 Linux Foundation 的技術項目推動。[^m]

## 版本沿革
| 版本 | 發布日期 | 主要變更 |
|---|---|---|
| ISO/IEC 5962 | 2021-09 取得認證[^m] | 成為國際標準 |
| 2.2 | 待補 | Microsoft sbom-tool 的預設輸出版本[^t] |
| 3.0（含 3.0.1） | 待補 | sbom-tool 以 `-mi SPDX:3.0` 支援；3.0 中文件 namespace 由 `namespaceMap` 表達[^t] |
| 其他版本 | 待補 | 待一手規格 |

## 資料模型與核心欄位
SPDX JSON 以 `packages[]` 列出套件（對照 CycloneDX 為 `components[]`）。[^sg] profile 設計與欄位細節待一手規格。

## 支援的序列化格式
- Tag:Value（`.spdx`）、JSON、XML、YAML、RDF；檔名慣例見 [[practices/sbom-file-naming]]。[^s1]
- 可在 .xlsx、.spdx、.xml、.json、.yaml 等格式間轉換。[^m]

## 與其他標準的比較
- Anchore 官方稱 SPDX 與 [[standards/cyclonedx|CycloneDX]] 為「兩種主要產業標準」。[^sg]
- 中文維基與資策會另列 [[standards/swid|SWID]] 為第三種格式。[^s4][^m]
- 兩者欄位結構差異與互轉：待補（參見未來的 `analyses/` 比較頁）。

## 工具生態系
- Syft 可輸出 SPDX JSON（`-o spdx-json=...`），見 [[tools/syft-grype]]。[^sg]
- Microsoft 與 Linux Foundation 提供以 SPDX 格式檢視軟體成分的工具。[^m]
- [[tools/microsoft-sbom-tool|Microsoft sbom-tool]] 專門輸出 SPDX 2.2／3.0，並可驗證。[^t]

## 採用狀況
資策會文章稱 NTIA 認可的機器可讀格式包含 SPDX（待對照 NTIA 原文）。[^m]

## 參考來源
[^t]: [[sources/2026-10-01-microsoft-sbom-tool]]
[^sg]: [[sources/2026-10-01-anchore-sbom-generation-guide]]
[^m]: [[sources/2026-10-01-moea-sbom-trends]]
[^s1]: [[sources/2026-10-01-openssf-sbom-naming]]
[^s4]: [[sources/2026-10-01-wikipedia-zh-software-supply-chain]]
