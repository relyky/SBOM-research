---
title: VEX（漏洞可利用性交換）
type: concept
tags: [sbom, vex, vulnerability]
aliases: [Vulnerability Exploitability eXchange]
sources: [raw/tools/sbom-tools.md, raw/tools/Grype.md, raw/industry/What Is VEX(Vulnerability Exploitability eXchange).md, raw/industry/Types of Software Bill of Material (SBOM) Documents.md, raw/tools/vexctl.md]
created: 2026-10-01
updated: 2026-10-06
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
- **OpenVEX 文件結構**：以 `@context`（如 `https://openvex.dev/ns/v0.2.0`）、`@id`、author、timestamp、version 與 `statements[]` 組成；每個 statement 含 `vulnerability`、`products[@id]`（purl）、`status`，可附 `justification`。[^v]
- **OpenVEX 狀態與理由**：來源範例出現 `not_affected`、`under_investigation`、`fixed`；`not_affected` 必須附 justification 或 impact statement；justification 範例有 `inline_mitigations_already_exist`、`vulnerable_code_not_in_execute_path`。[^v]
- **隨時間更新**：VEX 可先發 `under_investigation`，查明後再發 `not_affected` 或 `fixed`；[[tools/vexctl|vexctl]] 依時間順序重播多份文件算出現況，也能合併多個發布者的文件。[^v]
- **驗證**：讀取端通常忽略未知欄位，拼錯欄位會被默默丟棄，因此產出端需驗證（`vexctl validate`，可在 CI 以 `--strict` 把警告視為失敗）。[^v]
- **簽證與散布**：可包成 sigstore bundle／DSSE attestation 並以 OCI referrers API 附加到容器映像。[^v]
- **套用**：vexctl 的 `filter` 從 SARIF 掃描結果移除已 VEX 的項目（目前僅 SARIF）。[^v]
- **分享**：Aqua 的 VEX Hub 是集中儲存與下載 VEX attestation 的儲存庫。[^a]
- **類型脈絡**：CISA 認為 VEX 的進展可能促成新的 [[concepts/sbom-types|SBOM 類型]]。[^t]

## 相關概念
- [[concepts/sbom]]、[[concepts/cve]]、[[standards/cyclonedx]]

## 實務注意事項
- 容器與 Kubernetes 生態系對 VEX 的採用動能明顯。[^a]
- 以上多來自廠商文章與工具 README，CSAF／OpenVEX 規格本身仍待一手來源。
- [[tools/sbom-tools|sbom-tools]] 可疊加 OpenVEX（`--vex`），並用 `--fail-on-vex-gap` 在新引入漏洞缺 VEX 聲明時令 CI 失敗，也可偵測 SBOM 版本間 VEX 狀態轉變（如 NotAffected → Affected）。[^st]
- 不同格式的 justification 詞彙不同（CycloneDX：`code_not_reachable`；OpenVEX：`vulnerable_code_not_in_execute_path`），互轉時需對映。

## 開放問題
- `affected` 狀態與 justification 完整清單的語意（待驗證，vexctl README 僅示範部分）。
- 三種格式如何互轉？由誰產生 VEX 才可信？

## 參考來源
[^a]: [[sources/2026-10-01-aqua-what-is-vex]]
[^st]: [[sources/2026-10-06-sbom-tools-readme]]
[^t]: [[sources/2026-10-01-openssf-sbom-types]]
[^g]: [[sources/2026-10-01-anchore-grype-readme]]
[^v]: [[sources/2026-10-02-openvex-vexctl-readme]]
