---
title: 資策會 MIC：軟體物料清單 SBOM 發展趨勢
type: source
tags: [sbom, taiwan, trends]
sources: [raw/industry/軟體物料清單SBOM發展趨勢.md]
source_url: https://www.moea.gov.tw/MNS/doit/industrytech/IndustryTech.aspx?menu_id=13545&it_id=521
source_author: 楊淳安（資策會 MIC）
source_date: 2024-02-07
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# 資策會 MIC：軟體物料清單 SBOM 發展趨勢

## 基本資訊
- 類型：產業研究文章（經濟部產業技術司刊載）
- 作者/發布者：楊淳安，資策會產業情報研究所（MIC）
- 發布日期：2024-02-07
- 可信度評估：業界權威（台灣視角）；部分論述為二手轉述，需對照一手

## 重點摘要
1. 背景：SolarWinds（2020-12）、Colonial Pipeline（2021-05）、Log4j（2021-12）等事件，加上 Gartner 資料「90% 企業仰賴開源軟體」。
2. EO 14028（2021-05-12）共 8 項政策舉措，其中「強化軟體供應鏈安全」建議向聯邦政府銷售的軟體提供 SBOM。
3. NTIA 最低要素七項：供應商名稱、軟體套件名稱、套件版本、其他可識別套件之 ID、軟體供應鏈（依賴）關係、SBOM 作者、SBOM 產出時間。
4. 三種格式：SPDX（Linux Foundation，2021-09 取得 ISO/IEC 5962）、SWID（稱由 NIST 開發，2015 取得 ISO/IEC 19770-2）、CycloneDX（OWASP，專為 SBOM 設計，尚未取得 ISO 認證但為 NTIA 認可）。
5. 四類實作方案：雲端大廠（微軟 SBOM 工具、Google SLSA）、資服業者（anchore、Mend 等，台灣已有代理 Mend）、第三方組織（Software Transparency Foundation、Linux Foundation）、開源工具（Syft、Grype、Tern）。
6. 趨勢：容器／K8s 自動附帶 SBOM（Docker 2022 推出），促成由被動更新走向主動檢驗；軟體定義萬物下 SBOM 可能成為產業共識資安標準。
7. 建議：結合 DevSecOps，每次發布自動化產出 SBOM；台灣業者可結合弱點分析、修補建議、即時預警提供加值服務。

## 關鍵主張與數據
- 「NTIA進一步要求SBOM必須符合SPDX、SWID或CycloneDX任一格式」— 意涵：機器可讀格式的要求；用語「要求」待對照 NTIA 原文驗證。
- CNCF 調查：2022 年全球約 88% 企業在開發部署使用容器。

## 影響的 wiki 頁面
- [[regulations/ntia-minimum-elements]] — 補入七項資料欄位
- [[regulations/eo-14028]] — 補入 8 項政策舉措
- [[standards/swid]]、[[standards/spdx]]、[[standards/cyclonedx]] — 補充認證狀態
- [[tools/syft-grype]] — 新建
- [[concepts/sbom]]、[[concepts/software-supply-chain]]、[[overview]] — 補充台灣視角與趨勢

## 與既有知識的關係
- 支持：[[sources/2026-10-01-wikipedia-zh-software-supply-chain]] 的三種格式說法
- 矛盾：見 [[standards/swid]]（NIST 開發 vs ISO 定義）
- 新增：七項最低要素明細、產業方案分類、台灣市場觀察

## 待追問題
- 台灣官方規範（資安署、數發部、金管會）尚無一手來源。
- 文中所稱 NTIA「要求」三種格式之一，需查 NTIA 原文。
