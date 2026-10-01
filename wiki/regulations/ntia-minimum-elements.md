---
title: NTIA SBOM 最低要素
type: regulation
tags: [sbom, regulation, us, ntia]
aliases: [The Minimum Elements For a Software Bill of Materials, NTIA Minimum Elements]
sources: [raw/industry/Software supply chain.md, raw/industry/軟體供應鏈 - 維基百科，自由的百科全書.md, raw/industry/軟體物料清單SBOM發展趨勢.md]
jurisdiction: 美國
issuer: NTIA（美國國家電信暨資訊管理局）
effective_date: 2021-07-12（發布日）
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# NTIA SBOM 最低要素

> 本頁僅依二手來源撰寫；待取得 NTIA 原文（`raw/regulations/`）核對。截至 2026-10 的後續修訂（如 CISA 更新）尚未查證。

## 概述
依 [[regulations/eo-14028]] 要求，[[organizations/ntia|NTIA]] 於 2021-07-12 發布《The Minimum Elements For a Software Bill of Materials (SBOM)》，說明使 SBOM 讓供應鏈更透明的使用案例並列出後續演進選項。[^z]

## 適用對象與範圍
定義 SBOM 的最低內容與流程期望；適用範圍待一手來源。

## 對 SBOM 的具體要求
三大類：[^w][^z]
1. **資料欄位**：每個軟體元件的基線資訊
2. **自動化支援**：能以機器可讀與人類可讀格式產出；要求「自動生成」，可用 SCA 方案達成
3. **實務與流程**：組織何時、如何產生 SBOM

資料欄位的七項內容（資策會 MIC 整理）：[^m]
1. 供應商名稱
2. 軟體套件名稱
3. 套件版本
4. 其他可識別套件之 ID
5. 軟體供應鏈關係（依賴）
6. SBOM 作者
7. SBOM 產出時間

機器可讀格式：資策會文章稱 NTIA 要求符合 SPDX、SWID 或 CycloneDX 任一格式。[^m]（待驗證：「要求」或「認可」的用語，請對照 NTIA 原文。）

## 時程
| 日期 | 里程碑 |
|---|---|
| 2021-07-12 | NTIA 發布最低要素[^z] |

## 對企業的實務影響
- 自動化要求意味需將 SBOM 產生納入 CI/CD 與 SCA 工具鏈（推論，待驗證）。
- 標準化格式與自動化比對，可避免各廠商 SBOM 無法互相檢驗。[^m]

## 相關法規/指引
- [[regulations/eo-14028]]、[[concepts/sbom]]、[[concepts/sbom-types]]、[[standards/spdx]]、[[standards/cyclonedx]]、[[standards/swid]]

## 參考來源
[^w]: [[sources/2026-10-01-wikipedia-software-supply-chain]]
[^z]: [[sources/2026-10-01-wikipedia-zh-software-supply-chain]]
[^m]: [[sources/2026-10-01-moea-sbom-trends]]
