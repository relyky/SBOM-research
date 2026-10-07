---
title: Retire.js
type: tool
tags: [sbom, tool, sca, javascript, cyclonedx, owasp-top10]
sources: [raw/tools/RetireJS - repo.md, raw/tools/Retire.js - website.md]
vendor: RetireJS 專案
license: 來源未標示
version_checked: 未標示（README 提及 CycloneDX 1.7 輸出；截至 2026-10 剪藏）
created: 2026-10-02
updated: 2026-10-07
status: stub
---

# Retire.js

> 本頁僅依官方 README 與網站撰寫，尚無實測。

## 用途與定位
SCA 掃描器，偵測網頁與 Node.js 應用程式中「含已知漏洞版本」的 JavaScript 函式庫與 Node 模組；較新版本也能把找到的函式庫輸出為 CycloneDX SBOM。[^r][^w] 特點是能辨識不在套件清單內、直接下載放進版控的 JS 檔。[^r]

## 支援範圍
- 輸出格式：CycloneDX 1.4 XML（`cyclonedx`）；JSON 1.4／1.6／1.7；1.6、1.7 另有含 `vulnerabilities` 的 `_VEX` 變體。[^r]
- 語言/生態系：JavaScript／Node.js。[^r]
- 輸入來源：原始碼資料夾（CLI）、瀏覽中的網站（擴充套件）、站台（retire-site-scanner）。[^r]

## 基本用法
```bash
npm install -g retire
retire                                   # 掃描目前目錄
retire --outputformat cyclonedxJSON1_7   # 輸出 CycloneDX 1.7 JSON
retire --exitwith 0                      # 發現漏洞時不以 13 結束
```
（命令取自來源[^r]，尚未實測）

## CI/CD 整合
發現漏洞時預設 exit code 為 13，CI 可直接據此判定失敗；需改為不失敗時用 `--exitwith 0`。[^r] grunt、gulp 整合皆已 deprecated。[^r]

## 優缺點
- 優：專精前端 JS，可抓 vendored 檔案；有 Burp／ZAP 外掛與瀏覽器擴充可用於滲透測試與手動檢查。[^r][^w]
- 缺：僅涵蓋 JavaScript；與官方 [[tools/cyclonedx-npm]]（由 npm 依賴樹產生 BOM）的分工與清單差異尚未實測（對照為本庫推論）；漏洞資料來源與更新機制來源未說明；SBOM 功能網站未提及，僅見於 README。[^r][^w]

> [!warning] 矛盾
> Firefox 擴充套件：[[sources/2026-10-02-retirejs-website|官方網站]]列為四大組成之一；[[sources/2026-10-02-retirejs-repo|GitHub README]] 標為 **Deprecated**。Chrome 擴充套件在 README 註明「不在 Chrome 商店正式上架」，網站未提。判斷：網站內容較舊，以 README 為準。

## 漏洞資料
網站列出約 730 列「函式庫＋版本區間＋連結＋摘要」，連結以 GitHub Advisory（GHSA）約 583 筆為主，NVD 的 [[concepts/cve|CVE]] 約 64 筆。[^w]（筆數為本次對剪藏表格的粗略統計）

## 實測紀錄
（尚無）

## 參考來源
[^r]: [[sources/2026-10-02-retirejs-repo]]
[^w]: [[sources/2026-10-02-retirejs-website]]
