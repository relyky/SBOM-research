---
title: 以 syft + grype 為 .NET 專案產生 SBOM 並掃描漏洞
type: practice
tags: [sbom, practice, dotnet, syft, grype]
sources: [raw/tools/clonedx-dotnet.md, raw/tools/clonedx-dotnet-practice.md, raw/tools/sbom-tool.md, raw/tools/syft-grype.sample.md, raw/assets/publish.sbom.cdx.json, raw/assets/publish.grype.json]
created: 2026-10-01
updated: 2026-10-05
status: draft
---

# 以 syft + grype 為 .NET 專案產生 SBOM 並掃描漏洞

> 本頁依使用者 2026-10-01 的單次實測整理（syft 1.52.0、grype 0.119.0），結論僅限該專案，尚未跨專案驗證。

## 目標
為 .NET 專案產出 CycloneDX SBOM，並比對已知弱點；產物貼近實際部署內容。[^p]

## 適用情境
- .NET 應用程式，已有 `dotnet publish` 產物（含 `*.deps.json`）。[^p]
- 對應 [[concepts/sbom-types|SBOM 類型]]：掃描發佈產物屬於建置後分析（Analyzed 類）（對照分類為本庫推論，待驗證）。

## 流程步驟
1. 安裝並確認版本：`winget install Anchore.Syft`、`winget install Anchore.Grype`，重開終端機讓 PATH 生效。[^p]
2. 只掃發佈產物並指定名稱與版本（版本可取自 `publish/AsvtQUO.deps.json`）：[^p]
   ```bash
   syft dir:publish --source-name AsvtQUO --source-version 1.7.14-release -o cyclonedx-json=publish.sbom.cdx.json
   ```
3. 確認弱點資料庫：`grype db status`，必要時 `grype db update`。[^p]
4. 掃描 SBOM：`grype sbom:publish.sbom.cdx.json -o table`；需留存報告則 `-o json > ...`。[^p]
5. 檢視 JSON：`matches` 為比對結果、`ignoredMatches` 為被忽略項；兩者皆空即無已知弱點。[^p]

## 替代方案
- [[tools/microsoft-sbom-tool|Microsoft sbom-tool]]：以 `-bc` 掃 `*.csproj` 等專案檔、`-b` 雜湊出貨檔案，輸出 SPDX 2.2／3.0，可作為 .NET 工具安裝並含 validate。與 syft 的元件清單是否一致，尚未實測。[^t]

- [[tools/cyclonedx-dotnet|CycloneDX for .NET]]：`dotnet-CycloneDX <sln/csproj> -o <dir>` 從專案檔經 `dotnet restore` 解析依賴，輸出 CycloneDX 1.7；可用 `-ef` 排除不在出貨輸出的套件。使用者實測（6.2.0）：`dotnet-CycloneDX X.slnx -o .sbom -F Json -t -fn <檔名>`，預設輸出 XML、`-F Json` 才輸出 JSON；但未檢視 BOM 內容，與 syft 的元件清單是否一致尚未比較。[^c][^cp]

## 角色與責任
未定（來源為個人實測；導入時需明定由誰在 CI 產生、誰審閱結果）。

## 使用工具
- [[tools/syft-grype]]

## 檢核清單
- [ ] 只掃發佈產物，或用 `--exclude` 排除 `bin/`、`obj/`、`publish/` 的重複來源
- [ ] 設定 `--source-name` 與 `--source-version`，避免警告與以路徑推導 ID
- [ ] 記錄工具版本與弱點資料庫建置時間（本例 schema v6.1.9、built 2026-09-30）
- [ ] 確認 SBOM 內元件皆有 purl；清點無 purl 元件
- [ ] 保存 SBOM 與掃描結果

## 常見陷阱
- 掃整個專案目錄：1365 個元件，含重複計算；只掃發佈產物：176 個。[^p]
- grype 只比對有 purl 的套件，無 purl 的元件與 .NET 執行環境本身不在範圍；0 漏洞不等於安全。[^p]
- 缺授權資訊：使用者測得 syft 取不到 .NET 套件的授權資訊，無法快速檢查 license 是否核可，故改用 cyclonedx-dotnet 補此需求；實測 SBOM 亦無 license 欄位。[^cp]
- 實際 SBOM 檔：CycloneDX 1.7、170 個 `library`（皆 `pkg:nuget`）、6 個 `application`；各元件帶 CPE 與 `syft:*` 屬性。（本庫對附檔的直接檢視）[^p]

## 業界案例
（尚無）

## 參考來源
[^p]: [[sources/2026-10-01-syft-grype-dotnet-sample]]
[^t]: [[sources/2026-10-01-microsoft-sbom-tool]]
[^c]: [[sources/2026-10-05-cyclonedx-dotnet-readme]]
[^cp]: [[sources/2026-10-05-cyclonedx-dotnet-practice]]
