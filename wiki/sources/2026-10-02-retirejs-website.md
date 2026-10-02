---
title: Retire.js 官方網站
type: source
tags: [sbom, tool, sca, javascript, vulnerability]
sources: [raw/tools/Retire.js - website.md]
source_url: https://retirejs.github.io/retire.js/
source_author: Retire.js 專案
source_date: 未標示（剪藏於 2026-10-02）
created: 2026-10-02
updated: 2026-10-02
status: draft
---

# Retire.js 官方網站

## 基本資訊
- 類型：工具文件（專案網站）
- 作者/發布者：Retire.js 專案（retirejs.github.io）
- 發布日期：未標示
- 可信度評估：官方一手（工具定位與偵測範圍）；內容比 [[sources/2026-10-02-retirejs-repo|GitHub README]] 舊，部分描述已過時

## 重點摘要
1. 目的：偵測網頁與 Node.js 應用程式使用「含已知漏洞版本」的 JavaScript 函式庫；引用 OWASP Top 10 A06:2021（Vulnerable and Outdated Components）。[^w]
2. 網站列出四個組成：命令列掃描器、Chrome 擴充套件、Firefox 擴充套件、Burp／ZAP 外掛。[^w]
3. 約八成篇幅是「目前偵測的漏洞」表格，欄位為函式庫、起始版本、截止版本、連結、摘要（約 730 列資料）。[^w]
4. 漏洞連結以 GitHub Advisory（GHSA）為主（約 583 筆），其餘為 NVD 的 CVE（約 64 筆）。[^w]
5. 網站完全未提及 SBOM 產生功能。[^w]

## 關鍵主張與數據
- 「The goal of Retire.js is to help you detect use of version with known vulnerabilities.」— 意涵：本質是 SCA（軟體組成分析）掃描器，以「函式庫＋版本區間」比對漏洞。
- 漏洞表以版本區間（from／up to）描述影響範圍，例如 `@angular/core` 0 至 10.2.5 對應 GHSA-c75v-2vq8-878f（XSS）。— 意涵：資料庫以套件名稱＋版本範圍為鍵，不使用 [[concepts/sbom|SBOM]] 常見的 purl／CPE。

## 影響的 wiki 頁面
- [[tools/retire-js]] — 新增（定位、偵測範圍、漏洞資料來源）
- [[concepts/cve]] — 無更動（本來源的漏洞連結以 GHSA 為主，CVE 為輔，已記於工具頁）

## 與既有知識的關係
- 支持：[[tools/syft-grype]] 的「掃描器需要漏洞資料庫」模型；Retire.js 的差別在專精 JS 函式庫，連非套件管理器引入（直接下載、放進版控）的檔案也能辨識。
- 矛盾：網站稱 Firefox 擴充套件為正式組成，GitHub README 則標為 deprecated，且稱 Chrome 擴充套件不在官方商店；見 [[tools/retire-js]] 矛盾 callout。
- 新增：以 GHSA 為主的漏洞資料來源。

## 待追問題
- 漏洞資料庫（`jsrepository.json`）的更新頻率與維護方式？（網站未說明）
- 資料涵蓋的函式庫總數？（本次僅粗略解析表格，未精確統計）

[^w]: raw/tools/Retire.js - website.md
