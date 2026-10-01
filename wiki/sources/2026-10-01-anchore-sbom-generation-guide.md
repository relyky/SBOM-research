---
title: Anchore：SBOM Generation - Getting Started
type: source
tags: [sbom, tool, syft, guide]
sources: [raw/tools/SBOM Generation.md]
source_url: https://oss.anchore.com/docs/guides/sbom/getting-started/
source_author: Anchore
source_date: 2026-09-29（頁面最後修改）
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# Anchore：SBOM Generation - Getting Started

## 基本資訊
- 類型：工具文件（官方教學）
- 作者/發布者：[[organizations/anchore|Anchore]]
- 發布日期：頁面最後修改 2026-09-29
- 可信度評估：官方一手

## 重點摘要
1. 安裝：單一可執行檔、無外部相依；`curl`、`brew install syft`、`winget install Anchore.Syft`。
2. 預設只顯示最終映像（squashed）中的軟體；`--scope all-layers` 可納入所有層。
3. 同時輸出表格與 SPDX、CycloneDX 兩種「主要產業標準」：`-o table -o spdx-json=alpine.spdx.json -o cyclonedx-json=alpine.cdx.json`。
4. 以 `jq` 取套件：SPDX 用 `.packages[].name`，CycloneDX 用 `.components[].name`；Syft 預設單行 JSON，可設 `SYFT_FORMAT_PRETTY=true`。
5. FAQ：預設離線運作（`--enrich` 才會下載補充資訊）、不對外傳送任何資料、支援私有 registry、適合 CI/CD 自動化。

## 關鍵主張與數據
- 「Syft runs entirely locally and doesn't send any data to external services.」— 意涵：適合內網與資安敏感環境。
- 兩種格式欄位結構不同（`packages` vs `components`），消費端需分別處理。

## 影響的 wiki 頁面
- [[tools/syft-grype]]、[[standards/spdx]]、[[standards/cyclonedx]]

## 與既有知識的關係
- 支持：[[sources/2026-10-01-anchore-syft-readme]]
- 矛盾：無
- 新增：SPDX 與 CycloneDX 的 JSON 結構差異、`--scope` 行為

## 待追問題
- 掃描目錄時的重複計算與排除方式（見 [[practices/dotnet-sbom-syft-grype]]）。
