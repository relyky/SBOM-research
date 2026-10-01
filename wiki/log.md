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
