---
title: CycloneDX/cyclonedx-dotnet README
type: source
tags: [sbom, tool, cyclonedx, dotnet]
sources: [raw/tools/clonedx-dotnet.md]
source_url: https://github.com/CycloneDX/cyclonedx-dotnet
source_author: CycloneDX（GitHub 組織）
source_date: 未載明（剪藏日 2026-10-05）
created: 2026-10-05
updated: 2026-10-05
status: draft
---

# CycloneDX/cyclonedx-dotnet README

## 基本資訊
- 類型：工具文件
- 作者/發布者：CycloneDX GitHub 組織
- 發布日期：未載明；剪藏日 2026-10-05
- 可信度評估：官方一手（工具 README）
- 檔案瑕疵：「This module runs on」一句在剪藏中被截斷，支援平台不明。

## 重點摘要
1. 由 .NET 專案產生 CycloneDX BOM，彙整所有專案依賴；以 NuGet 全域工具（`dotnet tool install --global CycloneDX`，指令 `dotnet-CycloneDX`）或 Docker 映像發行。
2. 輸入可為 `.sln`／`.slnf`／`.slnx`／`.csproj`／`.fsproj`／`.vbproj`／`.xsproj`／`packages.config`，或遞迴掃描 packages.config 的目錄。
3. 預設輸出 CycloneDX 規格 1.7（`-spv` 可選 1.0–1.7），格式為 Auto／Json／UnsafeJson／Xml，預設檔名 `bom.xml` 或 `bom.json`。
4. 以 `dotnet restore` 解析依賴（可 `-dpr` 停用），可排除開發依賴（`-ed`）、測試專案（`-t`）與指定套件（`-ef`，連同其遞移依賴）。
5. 可透過 GitHub API 解析 SPDX 授權 ID（`-egl`）；未認證每小時 60 次，超限時 BOM 產生會失敗。
6. BOM metadata 優先序：CLI 參數（`--set-name`／`--set-version`／`--set-type`）> 範本檔（`--import-metadata-path`）> 由專案名稱自動推導；版本預設 `0.0.0`。
7. 憑證可由環境變數（`CYCLONEDX_NUGET_USERNAME` 等）提供，避免暴露於程序列表、shell 歷史與 CI 記錄；CLI 參數優先於環境變數。

## 關鍵主張與數據
- 「The exclude filter may be used to exclude any packages, which are resolved by NuGet, but do not exist in the final binary output.」— 意涵：與 [[tools/syft-grype|Syft]] 掃發佈產物的思路相同，需設法讓 SBOM 貼近實際部署內容，此工具改以排除過濾達成。
- 「`--set-nuget-purl`：Override the default BOM metadata component bom ref and PURL as NuGet package.」— 意涵：預設 metadata 主體不帶 NuGet purl，需旗標開啟，見 [[concepts/purl]]。
- Docker 範例建議 `--user $(id -u):$(id -g)`，未來大版本將預設非 root（README 引 ADR-001）。
- 貢獻環境需 .NET 8.0／9.0／10.0 SDK；CI 於 Windows、macOS、Linux 測試。

## 影響的 wiki 頁面
- [[tools/cyclonedx-dotnet]] — 新增
- [[standards/cyclonedx]] — 補 1.0–1.7 可選版本與 .NET 工具
- [[tools/microsoft-sbom-tool]] — 補 .NET 路線對照
- [[practices/dotnet-sbom-syft-grype]] — 補替代方案
- [[overview]]、[[index]]

## 與既有知識的關係
- 支持：[[overview]] 論點 8「.NET 生態系至少有兩條工具路線」，現增為三條。
- 矛盾：無。
- 新增：第一個以 CycloneDX 為輸出、從專案檔而非發佈產物解析 .NET 依賴的工具；預設規格版本 1.7，與 syft 1.52.0 實測一致。

## 待追問題
- 與 syft、sbom-tool 對同一 .NET 專案產出的元件清單是否一致？
- 解析自專案檔，是否涵蓋執行階段與自包含發佈的元件？
- README 引用的 `docs/best-practices.md`、`docs/bom-metadata.md` 尚未蒐集。
