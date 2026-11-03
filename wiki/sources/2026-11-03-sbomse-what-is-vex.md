---
title: sbom.se：What is VEX?
type: source
tags: [sbom, vex, vdr, csaf, openvex, cyclonedx]
sources: [raw/industry/What is VEX.md]
source_url: https://sbom.se/en/vulnerabilities/what-is-vex
source_author: Bitfront AB
source_date: 2025-02-07
created: 2026-11-03
updated: 2026-11-03
status: draft
---

# sbom.se：What is VEX?

## 基本資訊
- 類型：業界教學文章（短篇）
- 作者/發布者：Bitfront AB（sbom.se）
- 發布日期：2025-02-07
- 可信度評估：業界觀點；內容精簡，未引用規格原文。文中提到的 CISA VEX 最低要求「listed under References」，但剪藏未包含參考清單。

## 重點摘要
1. VEX 是供應商針對「產品是否受某漏洞影響」所做的機器可讀聲明。
2. 解決的問題：SBOM 比對漏洞資料庫會列出所有已知漏洞，但許多在該產品中無法利用；接收方很難自行判斷，供應商可以。
3. 四種狀態：Not Affected（不需行動）、Affected（建議行動）、Fixed（此版本已修復）、Under Investigation（尚未確定，後續更新）。
4. Not Affected 必須附理由，常見五種：元件不在產品中、漏洞程式碼不存在、漏洞程式碼不會執行、攻擊者無法控制漏洞程式碼、產品內既有防護可阻止利用。Affected 必須附建議行動（如升級到特定版本）。
5. SBOM 與 VEX 生命週期不同：某版本的 SBOM 不變，VEX 會隨新漏洞與評估改變而更新，因此通常分開提供。
6. VDR（Vulnerability Disclosure Report）列出產品所有已知漏洞與供應商分析；VEX 主要用來說明哪些漏洞「不」影響產品；VDR 可包含 VEX 資訊。
7. 三種格式：CSAF（OASIS 標準，有 VEX profile）、CycloneDX（可與 SBOM 同檔或另檔指向 SBOM，狀態名稱自成一套）、OpenVEX（OpenSSF 的獨立精簡格式）。CISA 發布了三種格式都能滿足的 VEX 最低要求。

## 關鍵主張與數據
- 「The recipient of an SBOM can rarely decide that alone. The supplier can.」— 意涵：VEX 的權威性來自供應商。
- 「The SBOM for a version does not change. VEX is updated when new vulnerabilities become known and when assessments change.」— 意涵：SBOM 與 VEX 分檔的理由。
- 「CycloneDX uses its own names for the statuses, such as `not_affected`, `exploitable`, `resolved` and `in_triage`.」— 意涵：跨格式互轉需要狀態對映。
- 「VEX is mainly used to state which vulnerabilities do not affect the product. A VDR can contain VEX information.」

## 影響的 wiki 頁面
- [[concepts/vex]] — 補四種狀態語意、not_affected 五種理由、Affected 須附行動、SBOM／VEX 生命週期、VDR、CSAF、CycloneDX 狀態名稱
- [[standards/cyclonedx]] — 補 CycloneDX VEX 狀態名稱與同檔／分檔
- [[organizations/openssf]] — OpenVEX 為 OpenSSF 專案
- [[organizations/cisa]] — 發布 VEX 最低要求

## 與既有知識的關係
- 支持：[[sources/2026-10-01-aqua-what-is-vex]] 的三種實作（OpenVEX／CSAF／CycloneDX）；[[sources/2026-10-02-openvex-vexctl-readme]] 的「not_affected 須附理由」與「隨時間更新」。
- 矛盾：將「元件不在產品中」列為 not_affected 理由，與 [[sources/2026-11-03-securebydesign-sbom-vex-workflows]]「元件存在但產品不受影響」的定義不一致（見 [[concepts/vex]]）。
- 新增：Affected 須附建議行動、VDR 概念、CycloneDX 狀態名稱、CISA VEX 最低要求的存在。

## 待追問題
- CISA《Minimum Requirements for VEX》原文。
- CSAF VEX profile、OpenVEX 規格本文；三種格式的 justification 詞彙對照。
- VDR 的定義（sbom.se 另有 what-is-vdr 頁）。
