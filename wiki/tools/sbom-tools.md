---
title: sbom-tools
type: tool
tags: [sbom, tool, cyclonedx, spdx, compliance, vex]
aliases: [sbom-tool/sbom-tools]
sources: [raw/tools/sbom-tools.md]
vendor: sbom-tool GitHub 組織（維護者未載明）
license: 未查證（README 摘錄未載明）
version_checked: 範例提及 v0.1.19（截至 2026-10 剪藏；1.0 前）
created: 2026-10-06
updated: 2026-10-06
status: stub
---

# sbom-tools

> stub：僅依官方 README 撰寫，尚無實測。**與 [[tools/microsoft-sbom-tool|Microsoft sbom-tool]] 是不同專案**（本工具為 Rust 開發，README 未列 SBOM 產生功能）。

## 用途與定位
SBOM／CBOM／AI-BOM 的「消費端」分析：語意 diff、品質評分、合規驗證、漏洞與 EOL 補強、機群查詢。README 未列從原始碼產生 SBOM 的功能（待驗證），範例以 [[tools/syft-grype|Syft]] 等產生器的輸出經管線串入。[^s]

## 支援範圍
- 輸入格式：CycloneDX 1.4–1.7、SPDX 2.2–2.3／3.0（JSON、JSON-LD、XML、tag-value、RDF/XML），自動偵測。[^s]
- 輸出格式：JSON、NDJSON、SARIF、OSCAL（`validate`）、sbomqs-JSON（`quality`）、HTML、Markdown、CSV、table、summary、TUI。[^s]
- 合規標準（16 種）：NTIA、CISA 2026、FDA、CRA Phase 1／2、SSDF、EO 14028、BSI TR-03183-2、EUCC、EU AI Act、PCI DSS 6.3.2、CISA FSCT 等。[^s]
- 漏洞資料：OSV、KEV；VEX 疊加支援 OpenVEX（見 [[concepts/vex]]）；EOL 用 endoflife.date。[^s]

## 基本用法
```bash
sbom-tools diff old.json new.json --enrich-vulns --fail-on-vuln -o sarif
sbom-tools validate sbom.json --standard ntia,cra,eo14028
sbom-tools quality sbom.json --profile security --min-score 70
sbom-tools query "log4j" --version "<2.17.0" fleet/*.json
syft -o cyclonedx-json . | sbom-tools quality - --profile security
```
（命令取自 README，尚未實測[^s]）

## CI/CD 整合
- 結束碼：1 變更／合規錯誤／品質不足、2 新漏洞、3 操作錯誤、4 VEX 缺口、5 授權違規、6 KEV 漏洞、7 ML 指標退步。[^s]
- 提供 GitHub Action（`sbom-tool/sbom-tools-action@v1`）與 SARIF 上傳範例。[^s]

## 優缺點
- 優：同一工具涵蓋 diff／品質／合規／查詢；可管線串接 syft、cosign；預編譯檔有 Sigstore 簽章。[^s]
- 缺／注意：
  - 1.0 前，JSON 輸出可能在 minor 版破壞相容，需鎖版本。[^s]
  - 合規通過不等於法規認證；CDXA 證明僅驗結構、不驗簽章。[^s]
  - 合規規則轉述自工具方，法規原文版本需自行核對。
  - 維護者背景與成熟度未載明（待查）。

## 實測紀錄
（尚無）

## 參考來源
[^s]: [[sources/2026-10-06-sbom-tools-readme]]
