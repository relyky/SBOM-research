---
title: Wikipedia：Common Vulnerabilities and Exposures（英文）
type: source
tags: [sbom, cve, vulnerability, wikipedia]
sources: [raw/industry/Common Vulnerabilities and Exposures.md]
source_url: https://en.wikipedia.org/wiki/Common_Vulnerabilities_and_Exposures
source_author: Wikipedia 編者
source_date: 2006-02-09（頁面建立；內容含 2026-03 資訊）
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# Wikipedia：Common Vulnerabilities and Exposures（英文）

## 基本資訊
- 類型：百科（二手彙整）
- 作者/發布者：Wikipedia 社群
- 發布日期：2006-02-09 建立；剪藏時間 2026-10-01
- 可信度評估：二手彙整，資金與營運狀態等時效資訊需回溯新聞原文

## 重點摘要
1. CVE 為公開資安弱點的參考編號系統，原名 Common Vulnerability Enumeration；由 MITRE 營運的 FFRDC 維護，資金來自美國 DHS 的 National Cyber Security Division；1999-09 正式對外推出。
2. 編號由 CVE Numbering Authority（CNA）指派；CNA 名稱與制度於 2005-02-01 確立。四類指派者：MITRE（編輯與主要 CNA）、各廠商 CNA、第三方協調者（如 CERT/CC）、研究者（個案）。
3. 編號語法 `CVE-YYYY-NNNN`，因應「CVE10k」問題，於 2015-01-13 起改為可變長度（4 位起，必要時擴增）。
4. CVE 涵蓋已公開發行軟體（含廣泛使用的 beta）；自訂且未散布的軟體、純服務類弱點歷來不給 CVE，但部分 CNA 已開始處理服務型弱點。
5. 指派爭議：廠商對回報有完全裁量，可能拒發 CVE；2023 宣布的「!CVE」計畫收集被廠商拒絕的弱點；也出現無安全影響的 CVE，許多開源專案因此申請成為自身的 CNA。
6. 資金風險：2025-04-15 報導 MITRE 與美國政府合約將到期，隨後延長 11 個月；依報導，2026-03-16 前後 CISA 代理局長表示該計畫已獲完整資金。

## 關鍵主張與數據
- 「CVE's common identifiers make it easier to share data across separate network security databases and tools」— 意涵：CVE ID 是跨工具比對弱點的共通鍵，SBOM 弱點比對依賴它。
- 「the contract ... was extended for 11 months, averting the shutdown of the program」

## 影響的 wiki 頁面
- [[concepts/cve]] — 新建
- [[organizations/mitre]] — 新建
- [[organizations/cisa]] — 補充 CVE 資金角色
- [[concepts/vex]]、[[concepts/sbom]] — 交叉引用

## 與既有知識的關係
- 支持：[[sources/2026-10-01-wikipedia-zh-cve]]
- 矛盾：無
- 新增：CNA 制度、語法變更、2025–2026 資金風險

## 待追問題
- NVD、OSV、CSAF 與 CVE 的關係與取捨（需另找來源）。
- 2026 年資金結論需查一手新聞。
