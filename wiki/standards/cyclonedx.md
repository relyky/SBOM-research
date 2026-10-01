---
title: CycloneDX
type: standard
tags: [sbom]
aliases: [CDX, ECMA-424]
sources: [raw/industry/軟體供應鏈 - 維基百科，自由的百科全書.md, raw/industry/Best Practices for Naming and Directory Conventions for SBOMs (Software Bill of Materials) in Open Source Projects.md]
created: 2026-10-01
updated: 2026-10-01
status: stub
---

# CycloneDX

> stub：僅有二手來源，尚未補齊 `templates/standard.md` 全部章節。

## 已知事實
- 由 OWASP 提出的 SBOM 格式。[^s4]
- 序列化格式與檔名慣例：JSON（`.cdx.json`）、XML（`.cdx.xml`），見 [[practices/sbom-file-naming]]。[^s1]

[^s1]: [[sources/2026-10-01-openssf-sbom-naming]]
[^s4]: [[sources/2026-10-01-wikipedia-zh-software-supply-chain]]

## 待回答問題
- 目前版本與主要變更（截至 2026）？
- 支援的 BOM 類型（SBOM、SaaSBOM、HBOM、ML-BOM、VEX…）？
- 各語言生態系的工具支援？
