---
title: "@cyclonedx/cyclonedx-npm（npm 套件頁 README）"
type: source
tags: [sbom, tool, cyclonedx, npm, nodejs]
sources: [raw/tools/cyclonedx-npm.md]
source_url: https://www.npmjs.com/package/@cyclonedx/cyclonedx-npm
source_author: CycloneDX（GitHub 組織，repo：CycloneDX/cyclonedx-node-npm）
source_date: 2026-08-11（剪藏 frontmatter 的 published；頁面稱最新版 6.0.1）
created: 2026-10-07
updated: 2026-10-07
status: draft
---

# @cyclonedx/cyclonedx-npm（npm 套件頁 README）

## 基本資訊
- 類型：工具文件
- 作者/發布者：CycloneDX GitHub 組織
- 發布日期：2026-08-11；剪藏日 2026-10-07
- 可信度評估：官方一手（工具 README，經 npmjs.com 顯示）
- 檔案瑕疵：剪藏含大量徽章圖片與錨點空連結，無內容影響。

## 重點摘要
1. 從 npm 專案產生 CycloneDX SBOM；自稱「probably the most accurate, complete SBOM generator for npm-based projects」（廠商自評）。
2. 依 OWASP SCVS 的 SBOM 條件，產出「almost passing Level-2」，僅簽章需外部完成。
3. 需求：`node >= 20.18.0`、`npm >= 9`；舊版工具支援 Node.js 14+／npm 6+。
4. 三種安裝：全域 `npm install --global`、`npx`、或專案 devDependency；指令 `cyclonedx-npm`。
5. 預設輸出 CycloneDX 1.6（可選 1.2–1.6）、JSON（可選 XML）、預設寫到 STDOUT；`-o` 指定檔案。
6. 以 npm 蒐集已安裝套件證據（`npm_execpath` 可覆寫 npm 執行檔）；`--package-lock-only` 可只讀 lockfile、不需 `node_modules`。
7. 不做人工去重：同一元件安裝多次會在 SBOM 中出現多次；`--flatten-components` 可攤平巢狀結構。
8. 支援 npm workspaces（標註為實驗性）、`--omit dev|optional|peer`、`--gather-license-texts`（實驗性，蒐集授權文字作為 license evidence）、`--short-PURLs`、`--output-reproducible`、`--validate`、`--mc-type`（application／firmware／library）。
9. 內部使用 CycloneDX JS 函式庫；無公開 API，僅 CLI 穩定；授權 Apache 2.0。

## 關鍵主張與數據
- 「this tool is capable of producing SBOM documents almost passing Level-2 (only signing needs to be done externally)」— 意涵：簽章需搭配其他工具，如 [[tools/cyclonedx-cli]] 的簽章功能（組合為本庫推論）。
- 「This tool does not do artificial deduplication.」— 意涵：元件數會高於不同套件數，與 syft 實測中重複元件現象類似，見 [[practices/dotnet-sbom-syft-grype]]。
- 「`--short-PURLs`：Omit all qualifiers from PackageURLs. This causes information loss」— 意涵：見 [[concepts/purl]]。

## 影響的 wiki 頁面
- [[tools/cyclonedx-npm]] — 新增
- [[standards/cyclonedx]] — 補 1.2–1.6 可選與 npm 工具
- [[overview]] — 論點 7 補 JS／npm 工具路線

## 與既有知識的關係
- 支持：[[standards/cyclonedx]] 官方生態系有各語言產生器（與 [[tools/cyclonedx-dotnet]] 同屬一系）。
- 矛盾：無。預設規格版本 1.6 低於 cyclonedx-dotnet 的預設 1.7，屬各工具版本差異，非衝突。
- 新增：npm 專屬的 lockfile-only、workspaces、reproducible 輸出選項。

## 待追問題
- 輸出 BOM 內容（元件數、授權欄位完整度）與 syft／Retire.js 掃同一 React／TypeScript 專案的差異。
- OWASP SCVS Level-2 具體條件。
- 是否支援 pnpm／yarn（頁面僅談 npm，未說明）。
