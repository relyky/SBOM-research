---
title: Aqua Security：What Is VEX（Vulnerability Exploitability eXchange）
type: source
tags: [sbom, vex, trivy]
sources: [raw/industry/What Is VEX(Vulnerability Exploitability eXchange).md]
source_url: https://www.aquasec.com/cloud-native-academy/vulnerability-management/vulnerability-exploitability-exchange/
source_author: The Cloud Native Experts（Aqua Security）
source_date: 2024-07-30
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# Aqua Security：What Is VEX

## 基本資訊
- 類型：廠商教學文章
- 作者/發布者：Aqua Security（Cloud Native Academy）
- 發布日期：2024-07-30
- 可信度評估：業界權威但有廠商立場（推廣 Trivy 與 VEX Hub）

## 重點摘要
1. VEX 是傳達「某弱點在特定產品／設定下是否可被利用」的標準化格式，供掃描工具使用，降低誤報。
2. VEX 由 NTIA 於 2021 年提出；與 SBOM 不同，VEX 只描述弱點，不描述元件資料，但可整合進 SBOM。
3. 三種主要實作：OpenVEX、CSAF VEX、CycloneDX VEX，語法不同但可傳達相同基本資訊。
4. 流程範例：用 Trivy 產出 CycloneDX SBOM，撰寫 VEX（對 CVE-2020-8911 標 `not_affected`、理由 `code_not_reachable`），再以 `trivy sbom ... --vex ...` 過濾結果。
5. 使用情境：供應商分享利用條件、減少掃描雜訊、辨識需避免的利用條件、稽核者評估實際可利用比例。
6. Aqua 建置 VEX Hub，作為 VEX attestation 的集中儲存庫。

## 關鍵主張與數據
- 「VEX only describes information about vulnerabilities, not other data about software supply chain components.」— 意涵：VEX 與 SBOM 互補而非取代。
- VEX 的 `affects.ref` 需對應 SBOM 的 serialNumber、version 與 bom-ref。

## 影響的 wiki 頁面
- [[concepts/vex]] — 由 stub 補成 draft
- [[tools/trivy]] — 新建
- [[standards/cyclonedx]] — 補充 CycloneDX VEX
- [[concepts/sbom]] — 補充 SBOM 與 VEX 的關係

## 與既有知識的關係
- 支持：[[sources/2026-10-01-openssf-sbom-types]] 提到 VEX 為潛在新類型
- 矛盾：無
- 新增：VEX 的實作格式與 Trivy 操作流程

## 待追問題
- OpenVEX、CSAF VEX 的規格與差異需一手來源。
- VEX 狀態值完整列表（本文只示範 `not_affected`）。
- VEX Hub 的涵蓋範圍與可信度。
