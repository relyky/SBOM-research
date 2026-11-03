---
title: Secure by Design Handbook：SBOM & VEX Workflows
type: source
tags: [sbom, vex, practice, cra, vulnerability]
sources: [raw/industry/SBOM & VEX Workflows.md]
source_url: https://www.securebydesignhandbook.com/docs/implementation/build-phase/sbom-vex
source_author: Secure by Design Handbook（作者未標示）
source_date: 未標示（剪藏於 2026-11-03）
created: 2026-11-03
updated: 2026-11-03
status: draft
---

# Secure by Design Handbook：SBOM & VEX Workflows

## 基本資訊
- 類型：業界實務指南（網站文件，屬 build phase 章節）
- 作者/發布者：Secure by Design Handbook 網站；作者、發布日期未標示
- 發布日期：未標示
- 可信度評估：業界指南；自述「engineering and product-security guidance. It is not legal advice」。法規條文為轉述，需對照原文。

## 重點摘要
1. SBOM 與 VEX 不只是掃描器產出的檔案，而是發布與漏洞處理流程的一環：元件清冊、漏洞監控、研判、受影響產品分析、修補、客戶溝通、證據保留。
2. 區分四種產物：SBOM（有哪些元件）、VEX（某漏洞是否影響此產品／版本）、Advisory（發生什麼、影響哪些版本、使用者該做什麼）、Vulnerability log（製造商知道、決定、修復、溝通、保留了什麼）。
3. 發布流程 8 步：定義範圍 → 產生 SBOM → 驗證涵蓋度 → 掃描漏洞 → 研判 → 發布閘門 → 保存證據 → 發布後監控；每步列出應保留的證據。
4. VEX 四種狀態（`under_investigation`、`not_affected`、`affected`、`fixed`）各需不同證據；沒有理由的 `not_affected` 是薄弱證據。
5. 9 道漏洞研判問題（元件是否存在、版本、程式碼是否編入、可達性、暴露面、既有緩解、受影響範圍、是否已知被利用、處置計畫）。
6. 法規脈絡：CRA 要求以 SBOM 辨識並記錄元件，BSI TR-03183-1 也要求記錄整合元件；CRA 並未限定 VEX 為唯一溝通格式。開機管理程式（boot manager）與 bootloader 應列為一級 SBOM 項目（ETSI EN 304 623 草案）。
7. 常見缺口：SBOM 未綁定發布、漏掉韌體／容器等元件、忽略遞移依賴、`not_affected` 無理由、修補後未更新 VEX、CI artifact 在支援期結束前就過期。

## 關鍵主張與數據
- 「An SBOM without a triage process can create noise. A VEX record without an accurate SBOM and vulnerability log is hard to trust.」— 意涵：SBOM、研判、VEX 三者缺一就不可信。
- 「The CRA does not make "VEX" the only permitted communication format.」— 意涵：VEX 是實務選擇，不是 CRA 的法定格式。
- 「the useful question is not just "did we produce an SBOM?" It is "can we quickly identify whether a vulnerability affects a product, version, customer, or support-period decision?"」— 意涵：SBOM 的價值在於能否快速回答影響範圍。
- 「retaining SBOMs in CI artifacts that expire before the product support period ends」被列為常見缺口 — 意涵：SBOM 的保存期限要對齊產品支援期。
- 「vulnerability scanning is repeated after release, not only at build time」— 意涵：與本庫「兩個迴圈」的作者建議一致。

## 影響的 wiki 頁面
- [[practices/vulnerability-triage-and-vex]] — 新建：發布流程、研判問題、證據清單、常見缺口
- [[concepts/vex]] — 補四種狀態所需證據、SBOM／VEX／Advisory／Vulnerability log 的區分、矛盾 callout
- [[regulations/eu-cra]] — 新建 stub（二手轉述）
- [[practices/sbom-lifecycle-and-ci]] — 加交叉連結，並註記業界指南的佐證
- [[overview]] — 新增論點

## 與既有知識的關係
- 支持：[[practices/sbom-lifecycle-and-ci]] 的「弱點 DB 更新後重掃既有 SBOM」作者建議；[[sources/2026-10-02-openvex-vexctl-readme]] 的「`not_affected` 必須附理由」。
- 矛盾：對 `not_affected` 的定義與 [[sources/2026-11-03-sbomse-what-is-vex]] 不一致（見 [[concepts/vex]] 的 warning）。
- 新增：CRA、BSI TR-03183-1、ETSI EN 304 623 等歐洲法規脈絡；韌體／bootloader 的涵蓋要求；證據保留觀點。

## 待追問題
- CRA 附件 I 第 II 部分第 1 點、第 13 條原文（EUR-Lex）。
- BSI TR-03183-1 REQ_VH 1 原文；與 sbom-tools 支援的 TR-03183-2 有何關係。
- ETSI EN 304 623 草案狀態。
- 文中引用的 Supply Chain Security Handbook、ENISA Supply-chain controls playbook 可作為後續來源。
