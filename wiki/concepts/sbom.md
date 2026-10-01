---
title: SBOM（軟體物料清單）
type: concept
tags: [sbom]
aliases: [Software Bill of Materials, 軟體物料清單, 軟體材料表]
sources: [raw/industry/軟體物料清單SBOM發展趨勢.md, raw/industry/What Is VEX(Vulnerability Exploitability eXchange).md, raw/industry/Software supply chain.md, raw/industry/軟體供應鏈 - 維基百科，自由的百科全書.md, raw/industry/Types of Software Bill of Material (SBOM) Documents.md]
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# SBOM（軟體物料清單）

## 定義
軟體物料清單（Software Bill of Materials, SBOM）宣告建置某個軟體製品所用的元件清冊，含開源與專有元件；是製造業物料清單（BOM）在軟體上的對應物，用以提升[[concepts/software-supply-chain|軟體供應鏈]]的透明度。[^s3] 中文維基以食品成份標籤類比。[^s4]

## 為什麼重要
- 建置者可確認元件為最新、對新漏洞快速反應；採購者可做漏洞與授權分析以評估風險。[^s3]
- 製造業利用 BOM 在部件有缺陷時找出受影響產品；SBOM 同理。[^s4]
- 採購端已開始要求：2023 年企業調查約 60–76% 要求或整合 SBOM 於採購與供應鏈風險管理（二手引用，待查原文）。[^s3]

## 運作方式 / 細節
- **最低要素**：資料欄位、自動化支援、實務與流程三類，見 [[regulations/ntia-minimum-elements]]。[^s3]
- **類型**：依資料來源分 Design / Source / Build / Analyzed / Deployed / Runtime，見 [[concepts/sbom-types]]。[^s2]
- **格式**：[[standards/spdx|SPDX]]（ISO/IEC 5962:2021）、[[standards/cyclonedx|CycloneDX]]（OWASP）、[[standards/swid|SWID]]。[^s4]
- **與 VEX／CVE**：SBOM 比對 [[concepts/cve|CVE]] 弱點後，可用 [[concepts/vex|VEX]] 標示「不可利用」以降低誤報。[^a]
- **趨勢（台灣視角，2024-02）**：容器與 Kubernetes 生態系自動附帶 SBOM（Docker 2022 推出），促成由被動更新走向主動檢驗；軟體定義萬物下，SBOM 可能成為產業共識的資安標準；建議結合 DevSecOps，每次發布自動產出。[^m]
- **儲存**：應集中於可被自動化系統查詢的儲存庫，而非試算表（無法自動以漏洞資料充實、難整合安全工具鏈）。[^s3]
- **完整性**：SBOM 提供可見性，不保證完整性；需搭配 provenance／簽章。[^s3]

## 相關概念
- [[concepts/software-supply-chain]]、[[concepts/sbom-types]]、[[concepts/vex]]
- [[practices/sbom-file-naming]]

## 實務注意事項
- 品質問題：研究指出 Java 生態系六種產生工具常產出膨脹、過度回報的依賴清單；不到半數專案於發布附 SBOM，且多不完整。[^s3]
- 開源專案採用率低：僅約 0.56% 熱門 GitHub 儲存庫含符合政策的 SBOM。[^s3]

## 開放問題
- 與 SCA 工具、傳統資產清冊的差異（尚無來源）。
- 在 Python / .NET / React / SQL Server 專案的產生方式（尚無來源）。

## 參考來源
[^a]: [[sources/2026-10-01-aqua-what-is-vex]]
[^m]: [[sources/2026-10-01-moea-sbom-trends]]
[^s2]: [[sources/2026-10-01-openssf-sbom-types]]
[^s3]: [[sources/2026-10-01-wikipedia-software-supply-chain]]
[^s4]: [[sources/2026-10-01-wikipedia-zh-software-supply-chain]]
