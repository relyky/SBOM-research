---
title: VEX（漏洞可利用性交換）
type: concept
tags: [sbom, vex, vulnerability]
aliases: [Vulnerability Exploitability eXchange]
sources: [raw/tools/sbom-tools.md, raw/tools/Grype.md, raw/industry/What Is VEX(Vulnerability Exploitability eXchange).md, raw/industry/Types of Software Bill of Material (SBOM) Documents.md, raw/tools/vexctl.md, raw/industry/What is VEX.md, raw/industry/SBOM & VEX Workflows.md]
created: 2026-10-01
updated: 2026-11-03
status: draft
---

# VEX（漏洞可利用性交換）

## 定義
標準化格式，用來傳達軟體產品中某弱點是否可被利用，並分享給掃描工具。[^a] 由 [[organizations/ntia|NTIA]] 於 2021 年提出。[^a] 另一種說法是：供應商針對「產品是否受某漏洞影響」所做的機器可讀聲明。[^se]

## 為什麼重要
掃描器找到弱點，不代表在特定設定下可被利用（例如需特定作業系統或啟用特定功能）。VEX 提供這層脈絡，讓團隊聚焦真正可利用的弱點、降低誤報，並使稽核者看到「可利用比例」而非弱點總數。[^a] SBOM 的接收方很難自行判斷，供應商可以，VEX 就是給出答案的格式。[^se]

不過 VEX 要可信，前提是有正確的 SBOM 與 vulnerability log；反過來，SBOM 若沒有研判流程，只會製造雜訊。[^h]

## 運作方式 / 細節
- **與 SBOM 的關係**：SBOM 描述元件（版本、來源）；VEX 只描述弱點，可整合進 SBOM，但不含其他元件資料。[^a]
- **SBOM、VEX、Advisory、Vulnerability log 的分工**：SBOM 回答「有哪些元件」；VEX 回答「某漏洞是否影響此產品／版本」；Advisory 回答「發生什麼、影響哪些版本、使用者該做什麼」；Vulnerability log 記錄製造商知道、決定、修復、溝通與保留了什麼。[^h]
- **生命週期不同**：某版本的 SBOM 不變，VEX 會隨新漏洞與評估更新，因此通常分開提供。[^se]
- **四種狀態**：[^se][^h]

  | 狀態 | 語意 | 所需內容／證據 |
  |---|---|---|
  | `not_affected` | 產品不受影響，不需行動[^se] | 必須附理由[^se][^v]；無理由是薄弱證據[^h] |
  | `affected` | 產品受影響，建議行動[^se] | 須附建議行動（如升級到特定版本）[^se]；影響分析、修補與溝通計畫[^h] |
  | `fixed` | 此版本已含修復[^se] | 修復版本、更新紀錄、release note、測試證據[^h] |
  | `under_investigation` | 尚不確定，後續會更新[^se] | 研判負責人、開始日期、審查中的產品[^h] |

- **not_affected 的常見理由**：元件不在產品中、漏洞程式碼不存在、漏洞程式碼不會執行、攻擊者無法控制漏洞程式碼、產品既有防護可阻止利用。[^se] Handbook 另列「設定停用」「平台不受影響」。[^h]

> [!warning] 矛盾：`not_affected` 是否涵蓋「元件不存在」
> - Secure by Design Handbook：`not_affected` 指「The vulnerable component is present, but the product is not affected」。[^h]
> - sbom.se：not_affected 的常見理由之一是「the component is not present in the product」。[^se]
> 兩者對「元件不存在」是否屬 not_affected 看法不同（Handbook 的研判問題第 1 題把「元件不存在」當成 SBOM 比對誤判處理）。以 OpenVEX／CSAF／CISA 規格原文為準，待驗證。

- **三種實作**：OpenVEX、CSAF VEX、CycloneDX VEX；語法不同，可傳達相同基本資訊。[^a] CSAF 是 OASIS 標準，有 VEX profile；OpenVEX 是 OpenSSF 的獨立精簡格式；CycloneDX VEX 可與 SBOM 同檔，也可另檔指向 SBOM，狀態名稱自成一套（如 `not_affected`、`exploitable`、`resolved`、`in_triage`）。[^se]
- **[[concepts/vdr|VDR]]**：VDR（Vulnerability Disclosure Report）列出產品所有已知漏洞與供應商分析；VEX 主要說明哪些漏洞「不」影響產品；VDR 可包含 VEX 資訊。[^se]
- **CISA 最低要求**：CISA 發布了三種格式都能滿足的 VEX 最低要求（原文未蒐集）。[^se]
- **法規地位**：[[regulations/eu-cra|CRA]] 並未把 VEX 定為唯一允許的溝通格式。[^h]
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
- [[concepts/sbom]]、[[concepts/cve]]、[[concepts/vdr]]、[[standards/cyclonedx]]

## 實務注意事項
- 容器與 Kubernetes 生態系對 VEX 的採用動能明顯。[^a]
- 以上多來自廠商文章與工具 README，CSAF／OpenVEX 規格本身仍待一手來源。
- [[tools/sbom-tools|sbom-tools]] 可疊加 OpenVEX（`--vex`），並用 `--fail-on-vex-gap` 在新引入漏洞缺 VEX 聲明時令 CI 失敗，也可偵測 SBOM 版本間 VEX 狀態轉變（如 NotAffected → Affected）。[^st]
- 研判流程、證據保留與發布閘門見 [[practices/vulnerability-triage-and-vex]]。[^h]
- 修補後要同步更新 VEX、公告與 release note，否則 VEX 會過時。[^h]
- 不同格式的 justification 詞彙不同（CycloneDX：`code_not_reachable`；OpenVEX：`vulnerable_code_not_in_execute_path`），互轉時需對映。

## 開放問題
- justification 完整清單與三種格式的詞彙對照（待規格原文；`affected` 語意已由 sbom.se 補充）。
- CISA《Minimum Requirements for VEX》原文。
- 三種格式如何互轉？由誰產生 VEX 才可信？

## 參考來源
[^a]: [[sources/2026-10-01-aqua-what-is-vex]]
[^st]: [[sources/2026-10-06-sbom-tools-readme]]
[^t]: [[sources/2026-10-01-openssf-sbom-types]]
[^g]: [[sources/2026-10-01-anchore-grype-readme]]
[^v]: [[sources/2026-10-02-openvex-vexctl-readme]]
[^se]: [[sources/2026-11-03-sbomse-what-is-vex]]
[^h]: [[sources/2026-11-03-securebydesign-sbom-vex-workflows]]
