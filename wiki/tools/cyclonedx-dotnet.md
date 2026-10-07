---
title: CycloneDX for .NET（cyclonedx-dotnet）
type: tool
tags: [sbom, tool, cyclonedx, dotnet]
aliases: [cyclonedx-dotnet, dotnet-CycloneDX, CycloneDX .NET tool]
sources: [raw/tools/clonedx-dotnet.md, raw/tools/clonedx-dotnet-practice.md, raw/tools/dotnet-sbom-scan.sh]
vendor: CycloneDX（GitHub 組織）
license: Apache 2.0
version_checked: 6.2.0（截至 2026-10，使用者實測安裝；預設規格版本 1.7）
created: 2026-10-05
updated: 2026-10-07
status: stub
---

# CycloneDX for .NET

> 本頁依官方 README 與使用者一次基本實測（僅指令與輸出路徑，未檢視 BOM 內容）撰寫。

## 用途與定位
從 .NET 專案產生 CycloneDX BOM，彙整專案所有依賴。[^s]

## 支援範圍
- 輸出格式：CycloneDX 1.0–1.7（預設 1.7）；JSON、XML、UnsafeJson（放寬跳脫）；預設檔名 `bom.xml`／`bom.json`。[^s]
- 語言/生態系：.NET（NuGet）；支援 C#、F#、VB 專案檔。[^s]
- 輸入來源：`.sln`／`.slnf`／`.slnx`／`.csproj`／`.fsproj`／`.vbproj`／`.xsproj`／`packages.config`，或遞迴掃描含 packages.config 的目錄。傳入方案檔會彙整所有專案。[^s]

## 基本用法
```bash
dotnet tool install --global CycloneDX
dotnet-CycloneDX YourSolution.sln -o /output/path
dotnet-CycloneDX MyProject.csproj -o /output/path -rs          # 遞迴掃專案參考
dotnet-CycloneDX MyProject.csproj -o /output/path -ef NETStandard.Library@1.6.0   # 排除套件
```
（命令取自 README，尚未實測[^s]）

- 重要選項：`-ed` 排除開發依賴、`-t` 排除測試專案、`-ef` 排除指定套件（含遞移依賴）、`-spv` 規格版本、`-F` 輸出格式、`-sn`／`-sv`／`-st` 覆寫 metadata 主體名稱／版本／類型、`--set-nuget-purl`、`-dpr` 停用 restore、`-dhc` 停用雜湊計算。[^s]
- Docker：`docker run --rm --user $(id -u):$(id -g) -v $(pwd):/work cyclonedx/cyclonedx-dotnet [OPTIONS] /work/<path>`。[^s]
- 若遇 command not found，重開終端機並確認 `~/.dotnet/tools` 在 `PATH`。[^s]

## BOM metadata
優先序：CLI 參數 > `--import-metadata-path` 範本 > 由專案名稱自動推導；版本預設 `0.0.0`、類型預設 Application。[^s]

## 授權解析與憑證
- 以 `-egl` 透過 GitHub API 解析 SPDX 授權 ID；未認證每小時 60 次，超限則 BOM 產生失敗；僅能解析 master 分支的授權檔參照。[^s]
- NuGet 私有來源與 GitHub 憑證可用環境變數（`CYCLONEDX_NUGET_USERNAME`／`_PASSWORD`、`CYCLONEDX_GITHUB_USERNAME`／`_TOKEN`／`_BEARER_TOKEN`、`GITHUB_TOKEN`）傳入，CLI 參數優先。[^s]

## CI/CD 整合
README 僅提到 GitHub Actions 情境下的 bearer token（`GITHUB_TOKEN`），未提供完整 pipeline 範例；細節見其 `docs/best-practices.md`（尚未蒐集）。[^s]

## 優缺點
- 優：原生輸出 CycloneDX（含 1.7）；可排除開發／測試依賴；可由環境變數注入憑證；Docker 可用。（來自 README 功能）[^s]
- 缺／注意：
  - 依賴由專案檔經 `dotnet restore` 解析，可能含實際不在出貨資料夾的套件（如 .NET Standard 遞移依賴），需用 `-ef` 手動排除。[^s]
  - 預設 metadata 版本為 `0.0.0`，需自行設定。[^s]
  - 授權解析：使用者實測選用本工具的原因是 syft 取不到 .NET 授權資訊；GitHub 授權解析另有 API 限額（見上）。[^p]
  - 與 [[tools/syft-grype|Syft]]（掃發佈產物）的清單差異尚未實測。（對照為本庫推論）

## 實測紀錄
選用動機：使用者測得 [[tools/syft-grype|syft]] 拿不到 .NET 套件的授權資訊，無法快速檢查 license 是否核可，而本工具對 .NET 套件支援較完整。[^p]（本庫檢視 syft 實測 SBOM 亦無授權欄位；本工具實際授權輸出尚未檢視）

腳本化：使用者以 `dotnet-CycloneDX WFAHRS.sln -o .sbom -fn <名>.cdx.json --json` 產出，再交給 [[tools/trivy]] 掃弱點與授權；此處用 `--json`，與上方 `-F Json` 寫法不同，兩者是否等價待查。[^sc] 見 [[practices/dotnet-sbom-cyclonedx-trivy]]。

2026-10-05，工具版本 6.2.0：[^p]
```bash
dotnet tool install --global CycloneDX      # 安裝後指令為 dotnet-CycloneDX
dotnet-CycloneDX QadbGraphQL.slnx -o .sbom  # 預設輸出 XML：.sbom\bom.xml
dotnet-CycloneDX QadbGraphQL.slnx -o .sbom -F Json -t -fn myproject-version-cdx.json
```
- 預設格式為 XML、預設檔名 `bom.xml`；要 JSON 需加 `-F Json`。[^p]
- `.slnx` 方案檔可直接使用。[^p]
- 自訂檔名 `myproject-version-cdx.json` 與 [[practices/sbom-file-naming]] 的 `.cdx.json` 慣例不同。（對照為本庫推論）
- 未檢視 BOM 內容（元件數、purl、規格版本），尚無法與 syft 比較。[^p]

## 參考來源
[^s]: [[sources/2026-10-05-cyclonedx-dotnet-readme]]
[^p]: [[sources/2026-10-05-cyclonedx-dotnet-practice]]
[^sc]: [[sources/2026-10-07-dotnet-sbom-scan-script]]
