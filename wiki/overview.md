---
title: SBOM 研究總覽
type: overview
tags: [sbom, overview]
sources: [raw/industry/Software supply chain.md, raw/industry/Types of Software Bill of Material (SBOM) Documents.md, raw/industry/Best Practices for Naming and Directory Conventions for SBOMs (Software Bill of Materials) in Open Source Projects.md]
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# SBOM 研究總覽

> 本頁是整個知識庫的「目前論點」。每次 ingest 若影響整體認知，LLM 需更新本頁。

## 研究問題
1. SBOM 是什麼、解決什麼問題？與傳統資產清冊、SCA（Software Composition Analysis）有何不同？
2. 主流格式（[[standards/spdx|SPDX]]、[[standards/cyclonedx|CycloneDX]]、SWID）差異為何？如何選擇？
3. 哪些法規/政策要求 SBOM？對台灣企業（含出口、供應鏈）的實際影響？
4. SBOM 的完整生命週期：產生 → 驗證 → 簽章 → 散布/交換 → 儲存 → 消費（漏洞比對、授權合規）→ 更新。
5. [[concepts/vex|VEX]] 如何與 SBOM 搭配，降低漏洞誤報？
6. 業界實際導入流程與成熟度：誰在做、怎麼做、遇到什麼困難？
7. 在 Python / .NET / React(TypeScript) / 容器專案中，如何在 CI/CD 自動產出並管理 SBOM？

## 目前論點
（截至 2026-10，基於 4 份業界／二手來源，尚無標準與法規一手資料，論點僅為初步。）

1. **SBOM 是供應鏈透明度的基礎，但非完整性保證**：它列出元件，需搭配 provenance／簽章才能驗證完整性。[^a]
2. **類型決定用途**：CISA 定義 Design / Source / Build / Analyzed / Deployed / Runtime 六類，產生方式不同，涵蓋與限制各異。見 [[concepts/sbom-types]]。[^b]
3. **政策驅動明確，實務落後**：EO 14028 與 NTIA 最低要素確立自動化等要求，但開源專案採用率與工具準確度仍有明顯缺口（如僅約 0.56% 熱門 GitHub 儲存庫含符合政策的 SBOM）。見 [[regulations/eo-14028]]、[[concepts/sbom]]。[^a]
4. **交換層面已有慣例**：JSON 為通用格式，檔名採「製品檔名 + `.cdx.json`／`.spdx.json`」。見 [[practices/sbom-file-naming]]。[^c]

[^a]: [[sources/2026-10-01-wikipedia-software-supply-chain]]
[^b]: [[sources/2026-10-01-openssf-sbom-types]]
[^c]: [[sources/2026-10-01-openssf-sbom-naming]]

## 研究路線圖（建議蒐集的來源）
以下為建議放入 `raw/` 的一手資料，ingest 後打勾：

**標準**（→ `raw/standards/`）
- [ ] SPDX 規格書（最新版）
- [ ] CycloneDX 規格說明與 Guide
- [ ] NTIA《The Minimum Elements for a Software Bill of Materials》

**政策與法規**（→ `raw/regulations/`）
- [ ] 美國行政命令 EO 14028（Improving the Nation's Cybersecurity）
- [ ] CISA SBOM 相關指引（最低要素更新、SBOM 類型、VEX 文件）
- [ ] 歐盟 Cyber Resilience Act（CRA）SBOM 相關條文
- [ ] FDA 醫療器材上市前網路安全指引
- [ ] 台灣相關規範（如資安署/數位發展部、金管會之供應鏈資安要求）

**工具**（→ `raw/tools/`）
- [ ] Syft / Grype、Trivy、cdxgen、Microsoft sbom-tool、CycloneDX 各語言外掛
- [ ] OWASP Dependency-Track、GUAC
- [ ] Sigstore / in-toto（簽章與證明）

**業界與案例**（→ `raw/industry/`、`raw/papers/`）
- [ ] Linux Foundation SBOM 採用調查報告
- [ ] OpenSSF 相關資源
- [ ] 企業導入案例、實務經驗分享

## 知識缺口
- （由 lint 填入）
