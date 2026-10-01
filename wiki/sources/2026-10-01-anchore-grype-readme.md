---
title: anchore/grype README
type: source
tags: [sbom, tool, grype, vex]
sources: [raw/tools/Grype.md]
source_url: https://github.com/anchore/grype
source_author: Anchore
source_date: 未標示（剪藏於 2026-10-01）
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# anchore/grype README

## 基本資訊
- 類型：工具文件（官方 README）
- 作者/發布者：[[organizations/anchore|Anchore]]
- 發布日期：未標示
- 可信度評估：官方一手

## 重點摘要
1. Grype 是針對容器映像與檔案系統的弱點掃描器，也可掃描 SBOM。
2. 支援主要作業系統套件生態（Alpine、Debian、Ubuntu、RHEL、Oracle Linux、Amazon Linux 等）與語言套件（Ruby、Java、JavaScript、Python、.NET、Go、PHP、Rust 等）。
3. 以 EPSS、KEV 與風險評分做威脅與風險優先排序。
4. 支援 [[concepts/vex|OpenVEX]]，可過濾與補強掃描結果。
5. 用法：`grype alpine:latest`、`grype ./my-project`；掃 SBOM：`grype sbom:./sbom.json` 或 `cat ./sbom.json | grype`（SBOM 掃描更快）。
6. 授權 Apache-2.0。

## 關鍵主張與數據
- 「OpenVEX support for filtering and augmenting scan results」— 意涵：VEX 已有主流掃描器支援（另見 [[tools/trivy]]）。

## 影響的 wiki 頁面
- [[tools/syft-grype]]、[[concepts/vex]]、[[concepts/cve]]

## 與既有知識的關係
- 支持：[[sources/2026-10-01-aqua-what-is-vex]]（VEX 可被掃描器消費）
- 矛盾：無
- 新增：EPSS／KEV 優先排序；OpenVEX 為 Grype 所支援的 VEX 格式

## 待追問題
- EPSS 與 KEV 的定義（尚無來源，屬背景知識待驗證）。
