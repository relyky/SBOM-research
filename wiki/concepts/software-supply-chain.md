---
title: 軟體供應鏈
type: concept
tags: [sbom, supply-chain]
aliases: [Software supply chain, 軟體供應鏈安全]
sources: [raw/industry/軟體物料清單SBOM發展趨勢.md, raw/industry/Software supply chain.md, raw/industry/軟體供應鏈 - 維基百科，自由的百科全書.md]
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# 軟體供應鏈

## 定義
開發、建置、發布軟體製品所用的元件、函式庫、工具與流程；借用實體商品供應鏈的類比。[^s3] 除函式庫外，還包含套件管理器（PyPI、npm）、工具（IDE、靜態分析器）與 SaaS（GitHub、AI 輔助開發產品）。[^s3]

## 為什麼重要
- 開源占比高：Synopsys 2024 分析 96% 商用程式碼庫含開源；Linux Foundation 2022 報告典型程式碼庫 70–90% 為開源元件。[^s3]
- Gartner 資料（經資策會 MIC 引用）稱 90% 企業仰賴開源軟體作為開發套件；與上述兩項的統計口徑是否相同，來源未說明，數字並列參考（推論，待驗證）。[^m]
- 觸發政策的事件：SolarWinds（2020-12）、Colonial Pipeline（2021-05）、Log4j（2021-12），促成 [[regulations/eo-14028]]。[^m]
- 攻擊上游元件可一次影響所有下游：SolarWinds（2020，逾 18,000 組織安裝惡意更新）、NotPetya（2017）、Kaseya（2021）、XZ Utils 後門（2024）。[^s3]
- Heartbleed、Shellshock（2014）與 Log4Shell（2021）顯示需要含 SCA 的漏洞管理。[^s3]

## 運作方式 / 細節
三個互補的安全屬性（引自 SoK 論文，經維基轉述）：[^s3]
- **Validity**：驗證貢獻者並保護製品與建置步驟不被竄改
- **Separation**：限制入侵可擴散的連線
- **Transparency**：向利害關係人揭露元件、貢獻者與流程

[[concepts/sbom|SBOM]] 列出依賴，provenance 紀錄如何建置；兩者提供可見性，但可見性本身不保證完整性。簽章式 attestation 可記錄製品來源、所用原始碼與依賴及建置步驟（例：in-toto）。[^s3]

## 相關概念
- [[concepts/sbom]]、[[concepts/vex]]、[[regulations/eo-14028]]

## 實務注意事項
- 供應鏈中的供應商與夥伴預設被隱性信任，是防護複雜之處。[^s3]
- 中文維基將相關條目列為：可重現構建、代碼簽名、供應鏈攻擊、相依性地獄等（尚未建頁）。[^s4]

## 開放問題
- Provenance／簽章工具（in-toto、Sigstore、SLSA）需專頁，待來源。

## 參考來源
[^s3]: [[sources/2026-10-01-wikipedia-software-supply-chain]]
[^s4]: [[sources/2026-10-01-wikipedia-zh-software-supply-chain]]
[^m]: [[sources/2026-10-01-moea-sbom-trends]]
