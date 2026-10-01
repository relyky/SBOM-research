---
title: CVE（公共漏洞和暴露）
type: concept
tags: [sbom, cve, vulnerability]
aliases: [Common Vulnerabilities and Exposures, 公共漏洞和暴露, 通用漏洞披露, CVE ID]
sources: [raw/industry/Common Vulnerabilities and Exposures.md, raw/industry/公共漏洞和暴露 - 維基百科，自由的百科全書.md]
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# CVE（公共漏洞和暴露）

## 定義
為公開已知資安弱點提供參考編號的系統，原名 Common Vulnerability Enumeration。由 [[organizations/mitre|MITRE]] 營運的 FFRDC 維護，資金來自美國 DHS；1999-09 正式對外推出。[^c]

## 為什麼重要
CVE ID 是跨弱點資料庫與安全工具共享資料的共通名稱，也是評估工具涵蓋度的基準；工具報告若含 CVE ID，可快速到各 CVE 相容資料庫查修補資訊。[^c] SCAP 與美國 NVD 皆使用 CVE ID。[^z] 這使它成為 [[concepts/sbom|SBOM]] 弱點比對與 [[concepts/vex|VEX]] 的基礎識別碼（VEX 範例即以 CVE-2020-8911 為對象）。

## 運作方式 / 細節
- **編號語法**：`CVE-YYYY-NNNN`；為解決「CVE10k」問題，2015-01-13 起改為可變長度（4 位起，必要時 5 位以上）。範例：Heartbleed 為 CVE-2014-0160。[^c][^z]
- **指派者**：由 CVE Numbering Authority（CNA）指派，2005-02-01 確立名稱與制度；分四類：MITRE（編輯與主要 CNA）、各廠商 CNA（如 Microsoft、Oracle、Red Hat）、第三方協調者（如 CERT/CC）、研究者（個案）。[^c]
- **範圍**：已公開發行軟體（含廣泛使用的 beta 與商用軟體）；未散布的自訂軟體歷來不給 CVE。服務型弱點原先不給，但部分 CNA 已開始處理。[^c]
- **狀態**：`RESERVED`（已保留未公開）、`REJECTED`（不符標準）；早期的「candidate（CAN-）」制度於 2005 年終止。[^c]
- 號段因多個編號機構而不一定連續。[^z]

## 相關概念
- [[concepts/vex]]、[[concepts/sbom]]、[[organizations/mitre]]、[[organizations/cisa]]

## 實務注意事項
- 廠商對回報有完全裁量，可拒發 CVE（利益衝突）；2023 宣布的「!CVE」計畫收集被廠商拒絕的弱點。也有無安全影響的 CVE。許多開源專案自己申請成為 CNA。[^c]
- 營運風險：2025-04 MITRE 與美國政府合約幾乎到期，後延長 11 個月；依報導，2026-03 前後已改列核心資金（截至 2026-10，需查新聞原文）。[^c]

## 開放問題
- NVD、OSV、CSAF 與 CVE 的關係（待來源）。
- CVE 覆蓋不到的弱點（如 npm、PyPI 生態系的 advisories）如何補（待來源）。

## 參考來源
[^c]: [[sources/2026-10-01-wikipedia-cve]]
[^z]: [[sources/2026-10-01-wikipedia-zh-cve]]
