---
title: NTIA SBOM 最低要素
type: regulation
tags: [sbom, regulation, us, ntia]
aliases: [The Minimum Elements For a Software Bill of Materials, NTIA Minimum Elements]
sources: [raw/industry/Software supply chain.md, raw/industry/軟體供應鏈 - 維基百科，自由的百科全書.md]
jurisdiction: 美國
issuer: NTIA（美國國家電信暨資訊管理局）
effective_date: 2021-07-12（發布日）
created: 2026-10-01
updated: 2026-10-01
status: stub
---

# NTIA SBOM 最低要素

> 本頁僅依二手來源撰寫；各資料欄位的具體清單待取得 NTIA 原文（`raw/regulations/`）。截至 2026-10 的後續修訂（如 CISA 更新）尚未查證。

## 概述
依 [[regulations/eo-14028]] 要求，NTIA 於 2021-07-12 發布《The Minimum Elements For a Software Bill of Materials (SBOM)》，說明使 SBOM 讓供應鏈更透明的使用案例並列出後續演進選項。[^s4]

## 適用對象與範圍
定義 SBOM 的最低內容與流程期望（適用範圍待一手來源）。

## 對 SBOM 的具體要求
三大類：[^s3][^s4]
1. **資料欄位**：每個軟體元件的基線資訊
2. **自動化支援**：能以機器可讀與人類可讀格式產出；要求「自動生成」，可用 SCA 方案達成
3. **實務與流程**：組織何時、如何產生 SBOM

## 時程
| 日期 | 里程碑 |
|---|---|
| 2021-07-12 | NTIA 發布最低要素[^s4] |

## 對企業的實務影響
自動化要求意味需將 SBOM 產生納入 CI/CD 與 SCA 工具鏈（推論，待驗證）。

## 相關法規/指引
- [[regulations/eo-14028]]、[[concepts/sbom]]、[[concepts/sbom-types]]

## 參考來源
[^s3]: [[sources/2026-10-01-wikipedia-software-supply-chain]]
[^s4]: [[sources/2026-10-01-wikipedia-zh-software-supply-chain]]
