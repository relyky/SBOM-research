---
title: SBOM 類型
type: concept
tags: [sbom, cisa, sbom-types]
aliases: [Types of SBOM, SBOM 文件類型]
sources: [raw/industry/Types of Software Bill of Material (SBOM) Documents.md, raw/industry/Best Practices for Naming and Directory Conventions for SBOMs (Software Bill of Materials) in Open Source Projects.md]
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# SBOM 類型

## 定義
即使最低內容要素相同，SBOM 會因資料來源不同而結果各異。[[organizations/cisa|CISA]] 文件定義六種類型，並說明類型未與軟體生命週期嚴格綁定，一份 SBOM 文件可合併多種類型的資訊。[^s2]

## 為什麼重要
選對類型決定能看到什麼：Source 看得到從未執行的元件，Runtime 看得到動態載入元件。產生、交換 SBOM 時應標明類型以避免誤用。

## 運作方式 / 細節

| 類型 | 定義（摘要） | 主要效益 | 主要限制 |
|---|---|---|---|
| Design | 新製品「預期設計」的元件清單（部分元件可能尚不存在），源自設計規格、RFP 或初始概念 | 購買授權前發現不相容元件；定義核准元件清單 | 難以產生；細節少 |
| Source | 由開發環境、原始檔與依賴產生，通常來自 SCA 工具加人工釐清 | 無需建置流程即可見；可在源頭修補；可見依賴樹 | 可能含未執行或被編譯排除的元件；可能漏掉執行期／外掛元件 |
| Build | 建置流程中產生，可整合中間的 Build 與 Source SBOM | 資訊正確性較高；涵蓋非原始碼元件；可與製品由同一建置流程簽章 | 可能需改建置流程；依賴建置環境；動態連結版本可能不準 |
| Analyzed | 建置後對製品（執行檔、套件、容器、VM 映像）分析而得，需啟發式方法；亦稱「第三方」SBOM | 不需開發環境或建置流程（如舊韌體）；可查核他方資料；可能找到隱藏依賴 | 可能遺漏、錯誤或近似 |
| Deployed | 系統上已安裝軟體的清冊，可由多份 SBOM 組合 | 呈現安裝元件與系統設定 | 可能需改安裝部署流程；可能無法反映執行環境 |
| Runtime | 對執行中系統插樁，只記錄實際存在的元件、外部呼叫與動態載入；亦稱 Instrumented／Dynamic | 看見實際使用中的元件與使用程度 | 需在執行中分析、有額外負擔；需運行一段時間才完整 |

（表格內容整理自 [^s2]）

## 相關概念
- [[concepts/sbom]]、[[concepts/vex]]
- [[practices/sbom-file-naming]] — 開源專案只維護 Source 與 Build；其他類型通常由消費者產生。[^s1]

## 實務注意事項
- 開源專案通常只負責 Source 與 Build SBOM；Deployed、Runtime 等多由軟體消費者維護。[^s1]
- CISA 預期未來可能新增類型：VEX、服務依賴、「SBOM of SBOMs」。[^s2]

## 開放問題
- 各工具（Syft、Trivy、cdxgen、sbom-tool）實際產出哪種類型？（待補工具來源）
- CycloneDX／SPDX 如何在欄位中標示類型（如 CycloneDX lifecycles）？（待驗證）

## 參考來源
[^s1]: [[sources/2026-10-01-openssf-sbom-naming]]
[^s2]: [[sources/2026-10-01-openssf-sbom-types]]
