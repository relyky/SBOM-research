---
title: 歐盟網路韌性法（CRA）
type: regulation
tags: [sbom, regulation, eu, cra]
aliases: [Cyber Resilience Act, CRA, Regulation (EU) 2024/2847]
sources: [raw/industry/SBOM & VEX Workflows.md, raw/tools/sbom-tools.md]
jurisdiction: 歐盟
issuer: 歐盟（發布機關待驗證）
effective_date: 待驗證
created: 2026-11-03
updated: 2026-11-03
status: stub
---

# 歐盟網路韌性法（CRA）

> stub：目前只有業界指南與工具 README 的二手轉述，尚無法規原文。

## 概述
網路韌性法（Cyber Resilience Act, CRA）。來源引用的 EUR-Lex 連結編號為 CELEX 02024R2847，推測為 Regulation (EU) 2024/2847（待驗證）。[^h]

## 適用對象與範圍
來源以「製造商（manufacturers）」為義務主體，並以聯網產品（connected-product）團隊為讀者。[^h] 適用產品範圍待原文。

## 對 SBOM 的具體要求
- 附件 I 第 II 部分第 1 點（Annex I, Part II § 1）：明確要求製造商辨識並記錄元件，包括製作 SBOM。[^h]
- 第 13 條（製造商義務）：主管機關（market surveillance authorities）要求時，須提供資訊與文件。[^h]
- CRA 並未把 VEX 定為唯一允許的溝通格式；VEX 是溝通漏洞狀態的實用標準化方式。[^h]
- 相關歐洲標準：BSI TR-03183-1 的 REQ_VH 1 要求記錄整合的元件；ETSI EN 304 623（草案）使開機管理程式的漏洞處理與支援期證據也變得重要。[^h]
- [[tools/sbom-tools]] 宣稱可做「CRA Phase 1／2」合規驗證，Phase 的定義待原文。[^st]

## 時程
| 日期 | 里程碑 |
|---|---|
| 待驗證 | 來源未提供生效與適用日期 |

## 對企業的實務影響
- SBOM 要綁定發布版本並保留至支援期結束，以便主管機關要求時能提出。[^h]
- 韌體、bootloader 等低階元件也應列入 SBOM。[^h]
- 實務流程見 [[practices/vulnerability-triage-and-vex]]。

## 相關法規/指引
- [[regulations/eo-14028]]、[[regulations/ntia-minimum-elements]]

## 參考來源
[^h]: [[sources/2026-11-03-securebydesign-sbom-vex-workflows]]
[^st]: [[sources/2026-10-06-sbom-tools-readme]]
