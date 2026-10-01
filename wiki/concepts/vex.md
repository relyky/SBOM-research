---
title: VEX（漏洞可利用性交換）
type: concept
tags: [sbom, vex, vulnerability]
aliases: [Vulnerability Exploitability eXchange]
sources: [raw/tools/Grype.md, raw/industry/What Is VEX(Vulnerability Exploitability eXchange).md, raw/industry/Types of Software Bill of Material (SBOM) Documents.md]
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# VEX（漏洞可利用性交換）

## 定義
標準化格式，用來傳達軟體產品中某弱點是否可被利用，並分享給掃描工具。[^a] 由 [[organizations/ntia|NTIA]] 於 2021 年提出。[^a]

## 為什麼重要
掃描器找到弱點，不代表在特定設定下可被利用（例如需特定作業系統或啟用特定功能）。VEX 提供這層脈絡，讓團隊聚焦真正可利用的弱點、降低誤報，並使稽核者看到「可利用比例」而非弱點總數。[^a]

## 運作方式 / 細節
- **與 SBOM 的關係**：SBOM 描述元件（版本、來源）；VEX 只描述弱點，可整合進 SBOM，但不含其他元件資料。[^a]
- **三種實作**：OpenVEX、CSAF VEX、CycloneDX VEX；語法不同，可傳達相同基本資訊。[^a]
- **CycloneDX VEX 範例**：以 `vulnerabilities[].analysis` 描述；範例為 `state: not_affected`、`justification: code_not_reachable`、`response: [will_not_fix, update]`。`affects.ref` 需對應 SBOM 的 serialNumber、version 與 bom-ref（如 purl）。[^a]
- **流程**：先產 SBOM，再撰寫 VEX，最後餵給掃描器過濾，例如 [[tools/trivy|Trivy]] 的 `--vex`。[^a]
- **掃描器支援**：[[tools/trivy|Trivy]] 以 `--vex` 套用；[[tools/syft-grype|Grype]] 支援 OpenVEX 以過濾與補強結果。[^g]
- **分享**：Aqua 的 VEX Hub 是集中儲存與下載 VEX attestation 的儲存庫。[^a]
- **類型脈絡**：CISA 認為 VEX 的進展可能促成新的 [[concepts/sbom-types|SBOM 類型]]。[^t]

## 相關概念
- [[concepts/sbom]]、[[concepts/cve]]、[[standards/cyclonedx]]

## 實務注意事項
- 容器與 Kubernetes 生態系對 VEX 的採用動能明顯。[^a]
- 以上多來自廠商文章，VEX 狀態值全集與 CSAF／OpenVEX 細節待一手規格。

## 開放問題
- 完整狀態值（not_affected、affected、fixed、under_investigation）的語意（待驗證，來源僅示範一種）。
- 三種格式如何互轉？由誰產生 VEX 才可信？

## 參考來源
[^a]: [[sources/2026-10-01-aqua-what-is-vex]]
[^t]: [[sources/2026-10-01-openssf-sbom-types]]
[^g]: [[sources/2026-10-01-anchore-grype-readme]]
