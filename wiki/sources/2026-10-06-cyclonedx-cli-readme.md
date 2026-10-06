---
title: CycloneDX/cyclonedx-cli README
type: source
tags: [sbom, tool, cyclonedx]
sources: [raw/tools/CycloneDX CLI tool for SBOM.md]
source_url: https://github.com/CycloneDX/cyclonedx-cli
source_author: CycloneDX（GitHub 組織）
source_date: 未載明（剪藏日 2026-10-06）
created: 2026-10-06
updated: 2026-10-06
status: draft
---

# CycloneDX/cyclonedx-cli README

## 基本資訊
- 類型：工具文件
- 作者/發布者：CycloneDX GitHub 組織
- 發布日期：未載明；剪藏日 2026-10-06
- 可信度評估：官方一手（工具 README）

## 重點摘要
1. 指令：`add`、`analyze`、`convert`、`diff`、`keygen`、`merge`、`sign`、`validate`、`verify`；涵蓋分析、修改、差異、合併、轉換、簽章與驗簽。
2. `convert` 支援 CycloneDX XML／JSON／Protobuf／CSV 與 SPDX JSON v2.3；輸出規格可選 v1_0–v1_7（CSV、SPDX 忽略）。
3. 轉換 SPDX ↔ CycloneDX 可能遺失資訊，由 `CycloneDX.Spdx.Interop`（CycloneDX.NET 函式庫）處理。
4. `validate` 預設以 v1.7 驗證，`--fail-on-errors` 令非零結束碼，可中斷建置；輸入／輸出皆可走 stdin／stdout（需指定格式）。
5. `merge` 支援 `--hierarchical`（需各 BOM 的 `metadata.component` 描述主體，並指定 `--name`、`--version`）。
6. 簽章：`keygen` 產生 RSA 金鑰對（PEM），`sign bom`／`sign file`（PKCS1 RSA SHA256）、`verify all`／`verify file`。
7. 官方支援 win-x64、linux-x64、linux-musl-x64、osx-x64；ARM 等為社群支援；亦有 Docker 映像與 Homebrew；需 .NET Core 執行階段；Apache 2.0。

## 關鍵主張與數據
- 「Converting between SPDX and CycloneDX formats can result in the loss of some information.」— 意涵：[[standards/spdx]] 與 [[standards/cyclonedx]] 互轉非無損。
- 「The CSV format is a limited representation of the list of components in a BOM.」— 意涵：CSV 只適合簡單使用，唯一必填為 `name`、`version`。
- 「`cyclonedx-cli validate --input-file sbom.xml --fail-on-errors`」— 意涵：可作 CI 閘門。

## 影響的 wiki 頁面
- [[tools/cyclonedx-cli]] — 新增
- [[standards/cyclonedx]]、[[standards/spdx]]、[[overview]]、[[index]]

## 與既有知識的關係
- 支持：[[standards/cyclonedx]] 的 1.0–1.7 版本範圍（同 [[tools/cyclonedx-dotnet]]）。
- 矛盾：無。
- 新增：第一個涵蓋簽章／驗簽、合併與 SPDX 互轉的 CycloneDX 官方 CLI；與 [[tools/cyclonedx-dotnet]]（產生）分工為「後處理」。

## 待追問題
- 實際版本號與發布日期未載明。
- 轉換 SPDX 時遺失哪些欄位（需看 CycloneDX.NET library 頁）？
- 簽章為 BOM 內嵌（JSF）或外部檔，與 Sigstore 路線的關係？
