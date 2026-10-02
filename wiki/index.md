---
title: 知識庫目錄
type: overview
tags: [index]
created: 2026-10-01
updated: 2026-10-02
---

# 知識庫目錄（Index）

> LLM 回答問題時先讀本頁。每次 ingest 後更新。格式：`- [[路徑|名稱]] — 一句話摘要（來源數，狀態）`

## 總覽
- [[overview|SBOM 研究總覽]] — 研究問題、目前論點、來源蒐集路線圖（19，draft）
- [[log|知識庫紀錄]] — 所有 ingest / query / lint 的時序紀錄

## 概念 Concepts
- [[concepts/sbom|SBOM]] — 軟體物料清單核心概念、用途、採用現況與趨勢（來源 6 份，draft）
- [[concepts/sbom-types|SBOM 類型]] — CISA 定義的六種 SBOM 類型與優缺點（來源 2 份，draft）
- [[concepts/software-supply-chain|軟體供應鏈]] — 定義、攻擊案例與三大安全屬性（來源 3 份，draft）
- [[concepts/vex|VEX]] — 漏洞可利用性交換，三種實作、OpenVEX 結構與 Trivy／vexctl 流程（來源 4 份，draft）
- [[concepts/purl|purl]] — Package URL，元件識別字串；grype 比對與 OpenVEX 產品識別的鍵（來源 3 份，stub）
- [[concepts/cve|CVE]] — 公共漏洞編號系統、CNA 制度與資金風險（來源 4 份，draft）

## 標準與格式 Standards
- [[standards/spdx|SPDX]] — SBOM 格式，ISO/IEC 5962，有 2.2、3.0 版（來源 5 份，stub）
- [[standards/cyclonedx|CycloneDX]] — OWASP 提出的 SBOM 格式，支援 VEX（來源 8 份，stub）
- [[standards/swid|SWID]] — ISO/IEC 19770-2 軟體識別標籤，NIST 推廣（來源 3 份，draft）

## 工具 Tools
- [[tools/trivy|Trivy]] — Aqua 開源掃描器，可產 SBOM 並套用 VEX（來源 1 份，stub）
- [[tools/microsoft-sbom-tool|Microsoft sbom-tool]] — Microsoft 的 SPDX 2.2／3.0 產生與驗證工具，有 .NET 工具版（來源 1 份，stub）
- [[tools/vexctl|vexctl]] — OpenVEX 專案的 CLI，建立／合併／驗證／簽證 VEX 並過濾 SARIF（來源 1 份，stub）
- [[tools/retire-js|Retire.js]] — 專精 JavaScript 函式庫的漏洞掃描器，可輸出 CycloneDX（含 VEX 變體）（來源 2 份，stub）
- [[tools/syft-grype|Syft / Grype]] — Anchore 開源 SBOM 產生、弱點與授權掃描工具，含 .NET 實測（來源 7 份，draft）

## 法規與政策 Regulations
- [[regulations/eo-14028|EO 14028]] — 美國 2021 年行政命令，催生 SBOM 最低要素（來源 3 份，stub）
- [[regulations/ntia-minimum-elements|NTIA 最低要素]] — 三大類與七項資料欄位（來源 3 份，draft）

## 組織 Organizations
- [[organizations/openssf|OpenSSF]] — SBOM Catalog 發布者（來源 2 份，stub）
- [[organizations/cisa|CISA]] — 發布 SBOM 類型指引的美國機關（來源 2 份，stub）
- [[organizations/nist|NIST]] — 推廣 SWID，EO 14028 下訂定指引（來源 2 份，stub）
- [[organizations/ntia|NTIA]] — 發布 SBOM 最低要素、提出 VEX（來源 3 份，stub）
- [[organizations/mitre|MITRE]] — 營運 CVE 系統（來源 2 份，stub）
- [[organizations/anchore|Anchore]] — Syft、Grype、Grant 的維護廠商（來源 3 份，stub）

## 實務流程 Practices
- [[practices/sbom-file-naming|SBOM 檔案命名慣例]] — 製品檔名加 `.cdx.json`／`.spdx.json` 等副檔名（來源 4 份，draft）
- [[practices/dotnet-sbom-syft-grype|.NET 專案以 syft + grype 產生 SBOM 並掃描]] — 掃發佈產物、指定名稱版本、注意 purl 限制（來源 4 份，draft）

## 來源摘要 Sources
- [[sources/2026-10-01-openssf-sbom-naming|OpenSSF：SBOM 命名與目錄慣例]] — 業界指引
- [[sources/2026-10-01-openssf-sbom-types|SBOM 文件類型（CISA）]] — 官方指引轉載
- [[sources/2026-10-01-wikipedia-software-supply-chain|Wikipedia：Software supply chain]] — 二手百科
- [[sources/2026-10-01-wikipedia-zh-software-supply-chain|維基百科：軟體供應鏈]] — 二手百科（繁中）
- [[sources/2026-10-01-nist-swid-tagging|NIST：SWID Tagging]] — 官方一手
- [[sources/2026-10-01-aqua-what-is-vex|Aqua：What Is VEX]] — 廠商教學文章
- [[sources/2026-10-01-moea-sbom-trends|資策會 MIC：SBOM 發展趨勢]] — 產業研究（台灣）
- [[sources/2026-10-01-wikipedia-cve|Wikipedia：CVE]] — 二手百科
- [[sources/2026-10-01-wikipedia-zh-cve|維基百科：公共漏洞和暴露]] — 二手百科（繁中）
- [[sources/2026-10-01-anchore-oss-overview|Anchore：開源工具總覽]] — 官方一手
- [[sources/2026-10-01-anchore-syft-readme|anchore/syft README]] — 官方一手
- [[sources/2026-10-01-anchore-grype-readme|anchore/grype README]] — 官方一手
- [[sources/2026-10-01-anchore-sbom-generation-guide|Anchore：SBOM Generation 教學]] — 官方一手
- [[sources/2026-10-01-anchore-vulnerability-scanning-guide|Anchore：Vulnerability Scanning 教學]] — 官方一手
- [[sources/2026-10-01-syft-grype-dotnet-sample|實測：syft + grype 掃描 .NET 專案]] — 使用者實測
- [[sources/2026-10-01-microsoft-sbom-tool|microsoft/sbom-tool README]] — 官方一手
- [[sources/2026-10-02-openvex-vexctl-readme|openvex/vexctl README]] — 官方一手
- [[sources/2026-10-02-retirejs-repo|RetireJS/retire.js README]] — 官方一手
- [[sources/2026-10-02-retirejs-website|Retire.js 官方網站]] — 官方一手（較舊）

## 分析 Analyses
- [[analyses/syft-grype-vexctl-workflow|syft → grype → vexctl 使用順序]] — 三工具串接的 mermaid 活動流程圖（來源 3 份，draft）
