---
title: CycloneDX BOM Standard（GitHub 組織首頁）
type: source
tags: [sbom, standard, cyclonedx, owasp]
sources: [raw/standards/CycloneDX BOM Standard.md]
source_url: https://github.com/CycloneDX
source_author: CycloneDX Core Working Group（OWASP）
source_date: 未載明（剪藏日 2026-10-06）
created: 2026-10-06
updated: 2026-10-06
status: draft
---

# CycloneDX BOM Standard（GitHub 組織首頁）

## 基本資訊
- 類型：規格（專案首頁，非規格本文）
- 作者/發布者：CycloneDX GitHub 組織
- 發布日期：未載明；剪藏日 2026-10-06
- 可信度評估：官方一手（但僅為概覽，無欄位級規格細節）

## 重點摘要
1. CycloneDX 自稱「full-stack BOM 標準」，規格涵蓋 SBOM、SaaSBOM、HBOM、ML-BOM、CBOM、MBOM、OBOM、VDR、VEX、CDXA 共 10 類。
2. 標準以 XML、JSON、Protocol Buffers 提供，另有官方與社群工具集（tool-center）。
3. 專案屬 OWASP，描述為「ratified as ECMA-424」；規格的策略方向與維護由 CycloneDX Core Working Group 負責，OWASP Foundation 支持。
4. 專案以 meritocracy 治理，並採風險導向的標準制定流程。

## 關鍵主張與數據
- 「CycloneDX is a OWASP project ratified as ECMA-424」（meta description）— 意涵：CycloneDX 已有 Ecma 國際標準編號 ECMA-424，處理了 [[standards/cyclonedx]] 先前「無來源、已移除」的別名。
- 「An accurate inventory of all components enables organizations to identify risk, allows for greater transparency, and enables rapid impact analysis.」— 意涵：官方給出的設計動機，與 [[concepts/sbom]] 的用途一致。

## 影響的 wiki 頁面
- [[standards/cyclonedx]] — 補 ECMA-424、BOM 類型清單、序列化格式（含 Protobuf）、治理
- [[organizations/owasp]] — 新增
- [[tools/cyclonedx-cli]]、[[overview]]、[[index]]

## 與既有知識的關係
- 支持：資策會稱 CycloneDX 由 OWASP 建構。
- 矛盾：無直接矛盾；補足資策會 2024-02「尚未取得 ISO 認證」之後的標準化狀態（ECMA-424 非 ISO，且批准時間本來源未載明）。
- 新增：BOM 類型遠超 SBOM；序列化含 Protocol Buffers。

## 待追問題
- ECMA-424 的批准日期與對應規格版本？
- CDXA（Attestations）、VDR 與 VEX 的欄位關係？
- 規格本文（`raw/standards/`）仍未取得。
