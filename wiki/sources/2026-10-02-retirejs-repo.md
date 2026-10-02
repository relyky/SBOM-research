---
title: RetireJS/retire.js README
type: source
tags: [sbom, tool, sca, javascript, cyclonedx]
sources: [raw/tools/RetireJS - repo.md]
source_url: https://github.com/retirejs/retire.js/
source_author: RetireJS 專案
source_date: 未標示（剪藏於 2026-10-02）
created: 2026-10-02
updated: 2026-10-02
status: draft
---

# RetireJS/retire.js README

## 基本資訊
- 類型：工具文件（官方 GitHub README）
- 作者/發布者：RetireJS 專案（github.com/RetireJS）
- 發布日期：未標示
- 可信度評估：官方一手（工具行為與選項）

## 重點摘要
1. 副標為「scanner detecting the use of JavaScript libraries with known vulnerabilities. Can also generate an SBOM of the libraries it finds.」[^r]
2. 設計動機：找出「不在套件清單（package manifests）內、只是下載後放進版控」的 JS 函式庫版本漏洞。[^r]
3. 七種使用方式：CLI、Chrome 擴充（非官方商店）、Burp／OWASP ZAP、Firefox 擴充（deprecated）、headless 站台掃描器 retire-site-scanner、grunt（deprecated）、gulp（deprecated）。[^r]
4. CLI 安裝與執行：`npm install -g retire` 後於專案目錄執行 `retire`。[^r]
5. SBOM 輸出：`retire --outputformat cyclonedx`（CycloneDX 1.4 XML）；JSON 用 `cyclonedxJSON`（1.4）、`cyclonedxJSON1_6`、`cyclonedxJSON1_7`；`_VEX` 變體（1_6、1_7）另含 `vulnerabilities` 區段。[^r]
6. 預設發現漏洞時 exit code 為 13，可用 `--exitwith 0` 覆寫。[^r]

## 關鍵主張與數據
- 「especially those that are not in package manifests, but simply downloaded and put in source control」— 意涵：補足 lockfile／manifest 型 SBOM 工具（如 [[tools/syft-grype|Syft]]）可能漏掉的 vendored JS。
- 「`cyclonedxJSON1_6_VEX` and `cyclonedxJSON1_7_VEX` variants also include a `vulnerabilities` section」— 意涵：同一份 [[standards/cyclonedx|CycloneDX]] 可同時帶元件與漏洞，與 [[concepts/vex]] 的 CycloneDX 實作相關。

## 影響的 wiki 頁面
- [[tools/retire-js]] — 新增
- [[standards/cyclonedx]] — 補 Retire.js 支援的版本與 VEX 變體
- [[overview]] — 補第 10 項論點、路線圖

## 與既有知識的關係
- 支持：[[standards/cyclonedx]] 的 VEX 支援說法。
- 矛盾：與 [[sources/2026-10-02-retirejs-website|官方網站]] 對 Firefox 擴充的狀態不一致（見 [[tools/retire-js]]）。
- 新增：專精 JS／前端函式庫的 SCA＋SBOM 工具；對本研究的 React／TypeScript 環境相關。

## 待追問題
- `_VEX` 輸出的 `vulnerabilities[].analysis` 是否填入可利用性判斷，或只列出漏洞？（README 未說明，待實測）
- 與 `cdxgen`、`npm sbom` 對同一 React 專案的元件清單差異？

[^r]: raw/tools/RetireJS - repo.md
