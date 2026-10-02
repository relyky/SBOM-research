---
title: 知識庫紀錄
type: overview
tags: [log]
created: 2026-10-01
updated: 2026-10-01
---

# 知識庫紀錄（Log）

> 只能 append。查詢最近紀錄：`grep "^## \[" wiki/log.md | tail -5`

## [2026-10-01] setup | 建立 SBOM 研究 LLM Wiki 骨架
- 依 Karpathy LLM Wiki 模式建立三層架構：`raw/`、`wiki/`、`CLAUDE.md`
- 建立頁面範本：source、concept、standard、tool、regulation、organization、practice、analysis
- 新增：[[overview]]、[[index]]，以及 stub 頁 [[concepts/sbom]]、[[concepts/vex]]、[[standards/spdx]]、[[standards/cyclonedx]]
- 下一步：依 [[overview]] 的研究路線圖蒐集第一批來源放入 `raw/`

## [2026-10-01] ingest | raw/industry 首批 4 份來源（OpenSSF 命名、CISA SBOM 類型、Wikipedia 軟體供應鏈中英文）
- 新增：[[sources/2026-10-01-openssf-sbom-naming]]、[[sources/2026-10-01-openssf-sbom-types]]、[[sources/2026-10-01-wikipedia-software-supply-chain]]、[[sources/2026-10-01-wikipedia-zh-software-supply-chain]]
- 新增：[[concepts/sbom-types]]、[[concepts/software-supply-chain]]、[[practices/sbom-file-naming]]、[[regulations/eo-14028]]、[[regulations/ntia-minimum-elements]]、[[organizations/openssf]]、[[organizations/cisa]]、[[standards/swid]]
- 更新：[[concepts/sbom]]、[[concepts/vex]]、[[standards/spdx]]、[[standards/cyclonedx]]、[[overview]]、[[index]]
- 備註：無直接矛盾；SWID「由 NIST 提出」僅見中文維基，已標待驗證。法規／標準頁僅有二手來源，需補一手資料。

## [2026-10-01] ingest | 第二批 5 份來源（NIST SWID、Aqua VEX、資策會 SBOM 趨勢、CVE 中英文）
- 新增：[[sources/2026-10-01-nist-swid-tagging]]、[[sources/2026-10-01-aqua-what-is-vex]]、[[sources/2026-10-01-moea-sbom-trends]]、[[sources/2026-10-01-wikipedia-cve]]、[[sources/2026-10-01-wikipedia-zh-cve]]
- 新增：[[concepts/cve]]、[[tools/trivy]]、[[tools/syft-grype]]、[[organizations/mitre]]、[[organizations/nist]]、[[organizations/ntia]]
- 更新：[[standards/swid]]（stub→draft）、[[concepts/vex]]（stub→draft）、[[regulations/ntia-minimum-elements]]（補七項欄位）、[[regulations/eo-14028]]、[[concepts/sbom]]、[[concepts/software-supply-chain]]、[[standards/spdx]]、[[standards/cyclonedx]]、[[organizations/cisa]]、[[overview]]、[[index]]
- 備註：矛盾已標示——[[standards/swid]]（NIST 一手頁稱 ISO 定義、NIST 推廣，MIC／中文維基稱 NIST 開發）；[[organizations/mitre]]（兩版維基的 FFRDC 名稱不同）。MIC 稱 NTIA「要求」三種格式之一，用語待對照原文。

## [2026-10-01] ingest | 第三批 Anchore 工具文件與 .NET 實測（raw/tools、raw/assets）
- 新增：[[sources/2026-10-01-anchore-oss-overview]]、[[sources/2026-10-01-anchore-syft-readme]]、[[sources/2026-10-01-anchore-grype-readme]]、[[sources/2026-10-01-anchore-sbom-generation-guide]]、[[sources/2026-10-01-anchore-vulnerability-scanning-guide]]、[[sources/2026-10-01-syft-grype-dotnet-sample]]
- 新增：[[practices/dotnet-sbom-syft-grype]]、[[organizations/anchore]]
- 更新：[[tools/syft-grype]]（stub→draft，納入 Grant 與實測）、[[standards/cyclonedx]]（實測見 specVersion 1.7）、[[standards/spdx]]、[[concepts/vex]]（Grype 支援 OpenVEX）、[[concepts/cve]]、[[concepts/sbom]]、[[overview]]、[[index]]
- 備註：無矛盾；資策會對 Syft／Grype 的二手描述獲官方文件支持。`publish.sbom.cdx.json`、`publish.grype.json`、`Anchore tools flow.png` 為輔助資料，併入對應來源頁而未各自建頁。決定保留單一 [[tools/syft-grype]] 頁而未拆成 syft、grype、grant 三頁（拆分需先徵得同意）。

## [2026-10-01] lint | 首次健康檢查（38 頁）
- 機械檢查：frontmatter 欄位、wikilink、孤兒頁、raw 未引用、來源路徑、腳註對應，皆無問題
- 發現：未經來源驗證的推論 1 項、章節偏離範本 2 頁、缺少交叉引用 1 項、反覆提及但無專頁的概念 5 項、時效資訊 2 項
- 備註：本次僅回報，未修改內容；待使用者同意後修正

## [2026-10-01] lint | 修正首次健康檢查的 4 項問題
- 更新：[[concepts/software-supply-chain]]（統計口徑改標推論待驗證）、[[standards/spdx]]、[[standards/cyclonedx]]（改依 templates/standard.md 章節，補 current_version／maintainer，移除無來源的 ECMA-424 別名）、[[practices/sbom-file-naming]]（補工具連結與實測檔名差異）、[[regulations/eo-14028]]（補時效聲明）
- 備註：purl／CPE、SCA、in-toto／SLSA、NVD／EPSS／KEV、Grant 等概念頁尚未建立，待使用者指定

## [2026-10-01] ingest | Microsoft sbom-tool README（raw/tools/sbom-tool.md）
- 新增：[[sources/2026-10-01-microsoft-sbom-tool]]、[[tools/microsoft-sbom-tool]]
- 更新：[[standards/spdx]]（補 2.2／3.0 版本線索）、[[practices/sbom-file-naming]]、[[practices/dotnet-sbom-syft-grype]]（補替代方案）、[[overview]]、[[index]]
- 備註：來源內部矛盾——標題稱 SPDX 2.2、內文稱 2.2 與 3.0，已於工具頁標示。資策會稱「微軟提供 SPDX 格式 SBOM 檢測工具」獲官方 README 支持。Component Detection、ClearlyDefined 尚無專頁。

## [2026-10-01] lint | 第二次健康檢查（40 頁）
- 發現：`raw/tools/` 整個目錄被移到 `raw/standards/tools/`（原因不明，疑為 Obsidian 拖曳），造成 41 筆 frontmatter `sources` 路徑失效、7 個 raw 檔案顯示未被引用
- 發現：index.md 6 個條目的來源數與頁面 frontmatter 不符（sbom、software-supply-chain、vex、cyclonedx、sbom-file-naming、dotnet-sbom-syft-grype）
- 備註：本次僅回報，未修改；raw/ 為人類擁有，待使用者決定移回或改路徑

## [2026-10-01] lint | 修正第二次健康檢查的問題
- 處理：`raw/standards/tools/` 移回 `raw/tools/`（依使用者同意），41 筆失效的 `sources` 路徑恢復
- 更新：[[index]]（6 個條目的來源數對齊頁面 frontmatter）

## [2026-10-02] ingest | openvex/vexctl README（raw/tools/vexctl.md）
- 新增：[[sources/2026-10-02-openvex-vexctl-readme]]、[[tools/vexctl]]
- 更新：[[concepts/vex]]（補 OpenVEX 結構、狀態值、justification、驗證、簽證、多文件重播）、[[overview]]、[[index]]
- 備註：無矛盾；CycloneDX 與 OpenVEX 的 justification 詞彙不同，已於 [[concepts/vex]] 註記。OpenVEX 規格、sigstore／cosign／in-toto 尚無專頁或一手來源。

## [2026-10-02] query | syft-grype-vexctl 使用順序流程圖
- 新增：[[analyses/syft-grype-vexctl-workflow]]
- 更新：[[index]]
- 備註：grype `--vex` 實際用法待驗證
