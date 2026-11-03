---
title: VDR（漏洞揭露報告）
type: concept
tags: [sbom, vdr, vex, vulnerability]
aliases: [Vulnerability Disclosure Report]
sources: [raw/industry/What is VEX.md, raw/standards/CycloneDX BOM Standard.md]
created: 2026-11-03
updated: 2026-11-03
status: stub
---

# VDR（漏洞揭露報告）

> stub：目前只有 sbom.se 的一段說明與 CycloneDX 官方首頁的 BOM 類型清單。

## 定義
漏洞揭露報告（Vulnerability Disclosure Report, VDR）列出產品所有已知漏洞，並附上供應商的分析。[^se]

## 為什麼重要
與 [[concepts/vex|VEX]] 互補：VEX 主要用來說明哪些漏洞「不」影響產品，VDR 則涵蓋全部已知漏洞；VDR 可包含 VEX 資訊。[^se]

## 運作方式 / 細節
- [[standards/cyclonedx|CycloneDX]] 將 VDR 列為支援的 10 類 BOM 之一。[^o] 欄位結構待規格本文。

## 相關概念
- [[concepts/vex]]、[[concepts/cve]]、[[concepts/sbom]]

## 實務注意事項
（尚無來源）

## 開放問題
- VDR 的正式定義出處與欄位結構（sbom.se 另有 what-is-vdr 頁，CycloneDX 規格本文待蒐集）。
- 實務上何時提供 VDR、何時只提供 VEX？

## 參考來源
[^se]: [[sources/2026-11-03-sbomse-what-is-vex]]
[^o]: [[sources/2026-10-06-cyclonedx-org-github]]
