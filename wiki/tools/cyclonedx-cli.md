---
title: CycloneDX CLI
type: tool
tags: [sbom, tool, cyclonedx]
aliases: [cyclonedx-cli]
sources: [raw/tools/CycloneDX CLI tool for SBOM.md]
vendor: CycloneDX（GitHub 組織）
license: Apache 2.0
version_checked: 未查證（README 未標版本，剪藏於 2026-10；支援規格至 v1.7）
created: 2026-10-06
updated: 2026-10-06
status: stub
---

# CycloneDX CLI

> stub：僅依官方 README 撰寫，尚無實測。

## 用途與定位
CycloneDX BOM 的「後處理」瑞士刀：分析、差異、合併、格式轉換、簽章與驗證；不負責從原始碼產生 BOM（產生見 [[tools/cyclonedx-dotnet]]）。[^s]

## 支援範圍
- 輸出格式：CycloneDX XML、JSON、Protobuf、CSV，以及 SPDX JSON v2.3；規格版本 v1_0–v1_7 可選。[^s]
- 語言/生態系：不限（只處理 BOM 檔）。
- 輸入來源：既有 BOM 檔或 stdin；`add files` 可由目錄產生檔案型 BOM。[^s]

## 基本用法
```bash
cyclonedx-cli validate --input-file sbom.xml --fail-on-errors
cyclonedx-cli convert --input-file sbom.xml --output-file sbom.json
cyclonedx-cli merge --input-files sbom1.xml sbom2.xml --output-file sbom_all.xml
cyclonedx-cli diff sbom-from.xml sbom-to.xml --component-versions
cyclonedx-cli analyze --input-file sbom.xml --multiple-component-versions
cyclonedx-cli keygen && cyclonedx-cli sign bom bom.json
```
（命令取自 README，尚未實測[^s]）

## CI/CD 整合
- 為自動化設計：有 `--input-file` 的指令可由 stdin 讀入，有 `--output-file` 者可輸出至 stdout（需指定格式）。[^s]
- `validate --fail-on-errors` 以非零結束碼中斷建置。[^s]

## 優缺點
- 優：官方出品；簽章／驗簽、合併、SPDX 互轉集中一個工具；有 Docker 映像、Homebrew。[^s]
- 缺／注意：
  - SPDX 互轉可能遺失資訊，SPDX 僅支援 JSON v2.3（不含 3.0）。[^s]
  - 需 .NET Core 執行階段；官方支援平台僅 x64（Windows、Linux、Linux musl、macOS）。[^s]
  - 差異／驗證的語意深度與 [[tools/sbom-tools]] 相比較淺（本庫推論，待實測）。

## 實測紀錄
（尚無）

## 參考來源
[^s]: [[sources/2026-10-06-cyclonedx-cli-readme]]
