---
title: SPDX
type: standard
tags: [sbom]
aliases: [Software Package Data Exchange, ISO/IEC 5962]
sources: [raw/industry/軟體供應鏈 - 維基百科，自由的百科全書.md, raw/industry/Best Practices for Naming and Directory Conventions for SBOMs (Software Bill of Materials) in Open Source Projects.md]
created: 2026-10-01
updated: 2026-10-01
status: stub
---

# SPDX

> stub：僅有二手來源，尚未補齊 `templates/standard.md` 全部章節。

## 已知事實
- 為 ISO/IEC 5962:2021 指定的 SBOM 格式。[^s4]
- 開放標準中提到自動化 SBOM 流程的需求。[^s4]
- 序列化格式與檔名慣例：Tag:Value（`.spdx`）、JSON、XML、YAML、RDF，見 [[practices/sbom-file-naming]]。[^s1]

[^s1]: [[sources/2026-10-01-openssf-sbom-naming]]
[^s4]: [[sources/2026-10-01-wikipedia-zh-software-supply-chain]]

## 待回答問題
- 目前版本與主要變更（截至 2026）？
- 資料模型與 profile 設計？
- 與 CycloneDX 的差異與互轉？
