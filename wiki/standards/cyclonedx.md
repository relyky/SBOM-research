---
title: CycloneDX
type: standard
tags: [sbom]
aliases: [CDX, ECMA-424]
sources: [raw/industry/軟體物料清單SBOM發展趨勢.md, raw/industry/What Is VEX(Vulnerability Exploitability eXchange).md, raw/industry/軟體供應鏈 - 維基百科，自由的百科全書.md, raw/industry/Best Practices for Naming and Directory Conventions for SBOMs (Software Bill of Materials) in Open Source Projects.md]
created: 2026-10-01
updated: 2026-10-01
status: stub
---

# CycloneDX

> stub：僅有二手來源，尚未補齊 `templates/standard.md` 全部章節。

## 已知事實
- 由 OWASP 提出的 SBOM 格式。[^s4]
- 建立之初即專為 SBOM 設計；截至資策會 2024-02 文章，尚未取得 ISO 認證，但為 NTIA 認可並推薦的格式之一。[^m]（ECMA-424 的認證狀態待驗證。）
- 支援 VEX（CycloneDX VEX，以 `vulnerabilities[].analysis` 描述可利用性），見 [[concepts/vex]]。[^a]
- 序列化格式與檔名慣例：JSON（`.cdx.json`）、XML（`.cdx.xml`），見 [[practices/sbom-file-naming]]。[^s1]

[^a]: [[sources/2026-10-01-aqua-what-is-vex]]
[^m]: [[sources/2026-10-01-moea-sbom-trends]]
[^s1]: [[sources/2026-10-01-openssf-sbom-naming]]
[^s4]: [[sources/2026-10-01-wikipedia-zh-software-supply-chain]]

## 待回答問題
- 目前版本與主要變更（截至 2026）？
- 支援的 BOM 類型（SBOM、SaaSBOM、HBOM、ML-BOM、VEX…）？
- 各語言生態系的工具支援？
