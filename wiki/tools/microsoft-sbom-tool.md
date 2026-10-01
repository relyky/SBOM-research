---
title: Microsoft sbom-tool
type: tool
tags: [sbom, tool, spdx, microsoft, dotnet]
aliases: [sbom-tool, Microsoft.SbomTool, Microsoft.Sbom.DotNetTool]
sources: [raw/tools/sbom-tool.md]
vendor: Microsoft
license: 未查證（README 摘錄未載明）
version_checked: 未查證（來源為 2026-10 剪藏，未標版本）
created: 2026-10-01
updated: 2026-10-01
status: stub
---

# Microsoft sbom-tool

> 本頁僅依官方 README 撰寫，尚無實測。

## 用途與定位
產生、驗證並（對 SPDX 2.2）去識別化 SBOM 的企業級工具；元件偵測靠 Component Detection，授權資訊靠 ClearlyDefined API。[^s]

> [!warning] 矛盾（來源內部）
> README 的 frontmatter 標題稱「create SPDX 2.2 compatible SBOMs」，內文與命令範例則為「SPDX 2.2 and SPDX 3.0」。本頁採內文說法，標題疑為較舊的 repo 描述（待驗證）。[^s]

## 支援範圍
- 輸出格式：SPDX 2.2（預設）、SPDX 3.0（`-mi SPDX:3.0`）；不輸出 CycloneDX（README 未提）。[^s]
- 語言/生態系：以專案檔判斷，README 舉例 `*.csproj`、`package.json`；完整清單見 Component Detection 文件（尚未蒐集）。[^s]
- 輸入來源：出貨資料夾（`-b`，會雜湊所有檔案）加原始碼資料夾（`-bc`）。[^s]

## 基本用法
```bash
# 產生（預設 SPDX 2.2；加 -mi SPDX:3.0 產生 3.0）
sbom-tool generate -b <drop path> -bc <build components path> -pn <package name> -pv <package version> -ps <package supplier> -nsb <namespace uri base>

# 驗證
sbom-tool validate -b <drop path> -o <output path> -mi SPDX:2.2

# 去除檔案參照（僅 SPDX 2.2）
sbom-tool redact -sp <path to the SBOM> -o <output path>
```
（命令取自 README，尚未實測[^s]）

- 預設輸出位置：`<drop path>\_manifest\spdx_2.2\manifest.spdx.json`（3.0 為 `spdx_3.0`）。[^s]
- 每份 SBOM 的 namespace 為 `<nsb>/<packageName>/<packageVersion>/<new-guid>`；`-nsb` 應為組織共用的 URI 前綴。[^s]
- 安裝：`winget install Microsoft.SbomTool`、`brew install sbom-tool`，或 .NET 工具 `dotnet tool install --global Microsoft.Sbom.DotNetTool`；亦有 `Microsoft.Sbom.Api` NuGet 套件。[^s]

## CI/CD 整合
官方提供 GitHub Actions 與 Azure DevOps Pipelines 的設定指南（指南內容尚未蒐集）。[^s]

## 優缺點
- 優：與 .NET 生態系貼近（可作 .NET 工具、提供 C# API）；同時提供 validate；SPDX 3.0 已支援。[^s]
- 缺／注意：
  - 只輸出 SPDX；若下游需要 CycloneDX（如 Aqua 流程的 VEX）需另用工具（如 [[tools/syft-grype|Syft]]）。（對照為本庫推論）
  - 不接受外部貢獻。[^s]
  - 預設輸出路徑與 [[practices/sbom-file-naming]] 的慣例不同。[^s]

## 實測紀錄
（尚無）

## 參考來源
[^s]: [[sources/2026-10-01-microsoft-sbom-tool]]
