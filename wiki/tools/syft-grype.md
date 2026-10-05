---
title: Syft / Grype
type: tool
tags: [sbom, tool, anchore]
aliases: [Syft, Grype, Grant, Tern, Anchore 開源工具]
sources: [raw/tools/Overview of Anchore Open Source tools.md, raw/tools/Syft.md, raw/tools/Grype.md, raw/tools/SBOM Generation.md, raw/tools/Vulnerability Scanning.md, raw/tools/syft-grype.sample.md, raw/tools/clonedx-dotnet-practice.md, raw/industry/軟體物料清單SBOM發展趨勢.md]
vendor: Anchore
license: Apache-2.0
version_checked: syft 1.52.0、grype 0.119.0（截至 2026-10，使用者實測）
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# Syft / Grype

## 用途與定位
[[organizations/anchore|Anchore]] 維護的三個開源 CLI（多為 Go，Apache-2.0）：[^o]
- **Syft**：SBOM 產生器與 Go 函式庫，掃描容器映像、檔案系統、封存檔。
- **Grype**：弱點掃描器，比對元件與已知弱點資料庫。
- **Grant**：授權掃描器，檢查映像、SBOM、檔案系統的授權並可對照自訂政策（本庫尚無用法資料）。

流程：Syft 產生一次 SBOM，Grype 與 Grant 各自獨立分析，分別產出弱點報告與授權報告。[^o] 另有資策會文章列出的 Tern 為同類開源 SBOM 產生工具（二手，未查證）。[^m]

## 支援範圍
- **輸出格式（Syft）**：[[standards/cyclonedx|CycloneDX]]、[[standards/spdx|SPDX]]、Syft JSON 等，可互轉；可用 in-toto 建立簽章 attestation。[^s]
- **語言／生態系**：Alpine（apk）、Debian（dpkg）、RPM、Go、Python、Java、JavaScript、Ruby、Rust、PHP、.NET 等。[^s] Grype 另涵蓋 Ubuntu、RHEL、Oracle Linux、Amazon Linux 等發行版。[^g]
- **輸入來源**：容器映像（OCI、Docker、Singularity）、檔案系統、封存檔；Grype 亦可直接掃 SBOM。[^s][^g]
- **風險排序**：Grype 以 EPSS、KEV 與風險評分排序，並支援 [[concepts/vex|OpenVEX]] 過濾。[^g]

## 基本用法
```bash
# 產生 SBOM（容器映像或目錄）
syft alpine:latest
syft dir:publish -o cyclonedx-json=publish.sbom.cdx.json

# 同時輸出多種格式
syft alpine:latest -o table -o spdx-json=alpine.spdx.json -o cyclonedx-json=alpine.cdx.json

# 掃描 SBOM
grype sbom:publish.sbom.cdx.json -o table
grype sbom:sbom.cdx.json -o json > sbom.grype.json

# 資料庫
grype db status
grype db update
```
（命令取自官方文件與使用者實測[^sg][^p]）

安裝：`winget install Anchore.Syft`、`winget install Anchore.Grype`；亦支援 curl 腳本、Homebrew 等。[^sg][^v]

## CI/CD 整合
官方稱兩者為自動化設計：建置時產生 SBOM，並可依嚴重度門檻讓 pipeline 失敗；兩者皆不對外傳送資料，Grype 資料庫下載後可離線掃描。[^v][^sg] 具體 CI 範例待補。

## 優缺點
- 優：單一執行檔、無外部相依、可離線；SBOM 產生與消費解耦；支援 .NET（NuGet）。[^sg][^p]
- 缺／注意：
  - 掃目錄會把 `bin/`、`obj/`、`publish/` 一併計入而重複計算，建議只掃發佈產物或用 `--exclude`。[^p]
  - Grype 只能比對有 purl 的套件，無 purl 的元件與 .NET 執行環境本身不在掃描範圍；結果 0 漏洞不代表無風險。[^p]
  - 授權資訊：使用者測得 syft 拿不到 .NET 套件的授權資訊，無法快速檢查 license 是否核可；本庫檢視實測 SBOM（`publish.sbom.cdx.json`）亦無任何 license 欄位。這也使依賴 SBOM 授權資料的 Grant 在 .NET 專案上的效用存疑（推論，待驗證）。[^cp]
  - 預設只掃最終映像（squashed），需 `--scope all-layers` 才含所有層。[^sg]

## 實測紀錄
2026-10-01，內部 .NET 專案 AsvtQUO（Windows 11 + Git Bash）：整個目錄 1365 個元件、發佈產物 176 個，兩者漏洞皆為 0。詳見 [[practices/dotnet-sbom-syft-grype]]。[^p]

## 參考來源
[^o]: [[sources/2026-10-01-anchore-oss-overview]]
[^s]: [[sources/2026-10-01-anchore-syft-readme]]
[^g]: [[sources/2026-10-01-anchore-grype-readme]]
[^sg]: [[sources/2026-10-01-anchore-sbom-generation-guide]]
[^v]: [[sources/2026-10-01-anchore-vulnerability-scanning-guide]]
[^p]: [[sources/2026-10-01-syft-grype-dotnet-sample]]
[^m]: [[sources/2026-10-01-moea-sbom-trends]]
[^cp]: [[sources/2026-10-05-cyclonedx-dotnet-practice]]
