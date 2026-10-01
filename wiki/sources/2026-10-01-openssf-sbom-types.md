---
title: SBOM 文件類型（CISA / OpenSSF 轉載）
type: source
tags: [sbom, cisa, sbom-types]
sources: [raw/industry/Types of Software Bill of Material (SBOM) Documents.md]
source_url: https://sbom-catalog.openssf.org/sbom-types.html
source_author: CISA（經 OpenSSF SBOM Catalog 轉載）
source_date: 未標示
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# SBOM 文件類型（CISA / OpenSSF 轉載）

## 基本資訊
- 類型：政府指引（轉載）
- 作者/發布者：[[organizations/cisa|CISA]]，由 [[organizations/openssf|OpenSSF]] SBOM Catalog 轉載；原文：https://www.cisa.gov/resources-tools/resources/types-software-bill-materials-sbom
- 發布日期：未標示
- 可信度評估：官方一手（內容）／轉載頁

## 重點摘要
1. 即使最低內容要素相同，SBOM 依資料來源不同會有不同結果，因而定義六種類型：Design、Source、Build、Analyzed、Deployed、Runtime。
2. 類型與生命週期階段並非嚴格綁定；一份 SBOM 文件可合併多種類型的資訊。
3. 每種類型各有效益與限制（見 [[concepts/sbom-types]]）。
4. 未來可能新增類型，例如 VEX、服務依賴、「SBOM of SBOMs」。

## 關鍵主張與數據
- 「An SBOM document may combine information for multiple SBOM types.」— 意涵：類型是描述資料來源的標籤，非互斥分類。
- Analyzed 類型「In some contexts, this may also be referred to as a '3rd party' SBOM.」；Runtime「Instrumented」或「Dynamic」SBOM。

## 影響的 wiki 頁面
- [[concepts/sbom-types]] — 新建
- [[concepts/sbom]] — 補充類型概念
- [[concepts/vex]] — 補充「VEX 可能成為新類型」
- [[organizations/cisa]] — 新建

## 與既有知識的關係
- 支持：[[sources/2026-10-01-openssf-sbom-naming]] 的範圍界定
- 矛盾：無
- 新增：六種類型的定義與優缺點

## 待追問題
- 原文發布日期與最新版本（本文轉載頁未標示）。
- 各類型對應的工具（Syft、Trivy、cdxgen 等）實際產出哪一類？
