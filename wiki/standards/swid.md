---
title: SWID
type: standard
tags: [sbom, standard, swid]
aliases: [Software Identification Tags, SWID Tags, ISO/IEC 19770-2]
sources: [raw/standards/Software Identification (SWID) Tagging.md, raw/industry/軟體物料清單SBOM發展趨勢.md, raw/industry/軟體供應鏈 - 維基百科，自由的百科全書.md]
current_version: ISO/IEC 19770-2:2015（截至 2026-04 NIST 頁面所述）
maintainer: ISO/IEC（標準）；NIST 負責推廣與指引
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# SWID

## 概述
軟體識別標籤（Software Identification Tag）是描述特定軟體產品版本的 tag 檔，由 ISO/IEC 19770-2:2015 定義，讓組織以透明方式追蹤受管裝置上已安裝的軟體。[^n] 生命週期為：安裝時加入 tag、解除安裝時刪除，因此 tag 存在即代表軟體存在。[^n]

> [!warning] 矛盾（歸屬說法不同）
> - NIST 官方頁：SWID「defined by the ISO/IEC 19770-2:2015 standard」，NIST 是「recommends adoption」的推廣方。[^n]
> - 資策會 MIC 與中文維基：稱 SWID「由 NIST 開發／提出」，2015 取得 ISO/IEC 19770-2。[^m][^z]
> - 暫時結論：以一手來源為準，標準由 ISO/IEC 定義、NIST 推廣；「NIST 開發」的說法保留但視為二手（待驗證）。

## 維護組織與治理
- 標準：ISO/IEC 19770-2:2015。[^n]
- 推廣：[[organizations/nist|NIST]]（Software Security Group，隸屬 Security Automation Program）；TCG 與 IETF 的標準已使用 SWID。[^n]

## 版本沿革
| 版本 | 發布日期 | 主要變更 |
|---|---|---|
| ISO/IEC 19770-2:2015 | 2015 | 定義 SWID Tag 與生命週期[^n][^m] |

## 資料模型與核心欄位
來源僅說明 tag 檔含「特定軟體產品版本的描述資訊」，欄位細節待一手規格。[^n]

## 支援的序列化格式
待補。

## 與其他標準的比較
- 被中文維基與 MIC 列為 SBOM 三種格式之一，另兩種為 [[standards/spdx]]、[[standards/cyclonedx]]。[^m][^z]
- 用途定位：NIST 描述的重點是「端點上已安裝軟體的清冊」（授權、修補、設定、預算）。[^n] 與 SBOM 以元件組成為主的定位有差異（推論，待驗證）。

## 工具生態系
NIST 已把 SWID 納入 SCAP 1.3，並規劃併入 NVD 弱點資料集。[^n]

## 採用狀況
資策會文章稱 NTIA 認可的機器可讀格式包含 SWID（待對照 NTIA 原文）。[^m]

## 參考來源
[^n]: [[sources/2026-10-01-nist-swid-tagging]]
[^m]: [[sources/2026-10-01-moea-sbom-trends]]
[^z]: [[sources/2026-10-01-wikipedia-zh-software-supply-chain]]
