---
title: SBOM 檔案命名慣例
type: practice
tags: [sbom, practice, naming, openssf]
sources: [raw/tools/sbom-tool.md, raw/tools/SBOM Generation.md, raw/tools/syft-grype.sample.md, raw/industry/Best Practices for Naming and Directory Conventions for SBOMs (Software Bill of Materials) in Open Source Projects.md]
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# SBOM 檔案命名慣例

## 目標
讓開源專案隨發布製品散布的 SBOM 檔名一致、可由製品檔名推得。[^s1]

## 適用情境
- 開源專案直接散布製品（tgz 原始碼、rpm、deb、zip 等），如 GitHub／GitLab Release；不適用於經 Maven、NPM 等生態系散布者。[^s1]
- 僅涵蓋 [[concepts/sbom-types|Source 與 Build]] 類型 SBOM。[^s1]
- 企業內部 SBOM 存放慣例：本來源未涵蓋（待補）。

## 流程步驟
1. 發布檔採扁平清單，不使用目錄結構。[^s1]
2. SBOM 檔名 = 製品完整檔名 + 標準副檔名（沿用 SLSA provenance 附加副檔名的作法）。[^s1]
3. 一律提供 JSON 版；如需其他格式，另外附上。[^s1]

| 標準＋格式 | SBOM 檔名（以 `artifact-1.0.0.tar.gz` 為例） |
|---|---|
| CycloneDX JSON | `artifact-1.0.0.tar.gz.cdx.json` |
| CycloneDX XML | `artifact-1.0.0.tar.gz.cdx.xml` |
| SPDX Tag:Value | `artifact-1.0.0.tar.gz.spdx` |
| SPDX JSON | `artifact-1.0.0.tar.gz.spdx.json` |
| SPDX XML | `artifact-1.0.0.tar.gz.spdx.xml` |
| SPDX YAML | `artifact-1.0.0.tar.gz.spdx.yml`（或 `.yaml`） |
| SPDX RDF | `artifact-1.0.0.tar.gz.spdx.rdf`（或 `.rdf.xml`） |

## 角色與責任
專案維護者負責 Source／Build SBOM；其他類型多由軟體消費者產生。[^s1]

## 使用工具
- 本來源未提及工具。可用 [[tools/syft-grype|Syft]] 以 `-o cyclonedx-json=<檔名>`、`-o spdx-json=<檔名>` 指定輸出檔名；[[standards/cyclonedx]]、[[standards/spdx]] 兩頁列有生態系工具。[^s5]
- 注意：Syft 官方範例（`alpine.cdx.json`）與使用者實測（`publish.sbom.cdx.json`）的檔名都未採本慣例的「製品完整檔名 + `.cdx.json`」。本慣例僅針對隨發布製品散布的 Source／Build SBOM，內部掃描檔未必適用；若要對外隨 release 發布，需自行改名。[^s5][^s6] [[tools/microsoft-sbom-tool|Microsoft sbom-tool]] 預設輸出到 `<drop path>\_manifest\spdx_2.2\manifest.spdx.json`，同樣不符。[^s7]

## 檢核清單
- [ ] SBOM 檔名以製品完整檔名開頭
- [ ] 副檔名為 `.cdx.*` 或 `.spdx.*`
- [ ] 提供 JSON 版
- [ ] 不使用子目錄

## 常見陷阱
- 發布於生態系（Maven、PyPI 等）時，不預期把此 SBOM 上傳至該生態系。[^s1]

## 業界案例
（尚無）

## 參考來源
[^s1]: [[sources/2026-10-01-openssf-sbom-naming]]
[^s5]: [[sources/2026-10-01-anchore-sbom-generation-guide]]
[^s6]: [[sources/2026-10-01-syft-grype-dotnet-sample]]
[^s7]: [[sources/2026-10-01-microsoft-sbom-tool]]
