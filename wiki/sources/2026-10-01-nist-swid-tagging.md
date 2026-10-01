---
title: NIST：Software Identification (SWID) Tagging 專案頁
type: source
tags: [sbom, swid, nist]
sources: [raw/standards/Software Identification (SWID) Tagging.md]
source_url: https://csrc.nist.gov/projects/software-identification-swid
source_author: NIST Computer Security Division, Software Security Group
source_date: 2026-04-13（頁面更新日）
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# NIST：Software Identification (SWID) Tagging 專案頁

## 基本資訊
- 類型：官方專案說明
- 作者/發布者：[[organizations/nist|NIST]] 電腦安全部門 Software Security Group
- 發布日期：頁面更新於 2026-04-13
- 可信度評估：官方一手

## 重點摘要
1. 動機：企業需要準確的軟體清冊，用於授權合規、符合政策、確認已修補、確認安全設定、規劃投資。
2. SWID Tag 由 ISO/IEC 19770-2:2015 定義，描述特定軟體產品版本；標準定義的生命週期是安裝時加入 tag、解除安裝時刪除，使 tag 的存在對應軟體的存在。
3. NIST 建議軟體生產者採用；TCG 與 IETF 的標準已使用 SWID Tag。
4. NIST 規劃把 SWID 資料納入 NVD 弱點資料集，且 SCAP 1.3 已納入 SWID。

## 關鍵主張與數據
- 「Software Identification (SWID) Tags, defined by the ISO/IEC 19770-2:2015 standard」— 意涵：SWID 的標準歸屬是 ISO/IEC，NIST 是推廣者。
- 「The National Institute of Standards and Technology recommends adoption of the SWID Tag standard by software producers」

## 影響的 wiki 頁面
- [[standards/swid]] — 由 stub 補成 draft，解決先前「待驗證」
- [[organizations/nist]] — 新建

## 與既有知識的關係
- 支持：[[sources/2026-10-01-moea-sbom-trends]] 的 ISO/IEC 19770-2（2015）說法
- 矛盾：見 [[standards/swid]] 的矛盾 callout（「NIST 開發」vs「ISO 定義」）
- 新增：SWID 的生命週期設計與 SCAP／NVD 整合

## 待追問題
- SWID 與 SBOM 格式（SPDX／CycloneDX）在用途上的差異：SWID 偏安裝端清冊，SBOM 偏元件組成（推論，待驗證）。
