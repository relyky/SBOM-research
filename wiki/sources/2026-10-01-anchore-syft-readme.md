---
title: anchore/syft README
type: source
tags: [sbom, tool, syft]
sources: [raw/tools/Syft.md]
source_url: https://github.com/anchore/syft
source_author: Anchore
source_date: 未標示（剪藏於 2026-10-01）
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# anchore/syft README

## 基本資訊
- 類型：工具文件（官方 README）
- 作者/發布者：[[organizations/anchore|Anchore]]
- 發布日期：未標示
- 可信度評估：官方一手

## 重點摘要
1. Syft 是從容器映像與檔案系統產生 SBOM 的 CLI 工具與 Go 函式庫，搭配 Grype 可做弱點偵測。
2. 掃描目標：容器映像、檔案系統、封存檔；支援數十種套件生態系（apk、dpkg、RPM、Go、Python、Java、JavaScript、Ruby、Rust、PHP、.NET 等）；支援 OCI、Docker、Singularity 映像。
3. 輸出格式：CycloneDX、SPDX、Syft JSON 等，可在格式間轉換。
4. 可用 in-toto 規格建立簽章的 SBOM attestation。
5. 基本用法：`syft alpine:latest`、`syft ./my-project`、`syft <image> -o cyclonedx-json`、多格式同時輸出 `-o spdx-json=./spdx.json -o cyclonedx-json=./cdx.json`。
6. 安裝：`curl -sSfL https://get.anchore.io/syft | sudo sh -s -- -b /usr/local/bin`，亦支援 Homebrew、Docker、Scoop、Chocolatey、Nix 等。
7. 授權 Apache-2.0；商業支援需聯繫 Anchore。

## 關鍵主張與數據
- 「Create signed SBOM attestations using the in-toto specification」— 意涵：與 [[concepts/software-supply-chain|供應鏈]]的 provenance／簽章做法銜接。

## 影響的 wiki 頁面
- [[tools/syft-grype]]、[[standards/cyclonedx]]、[[standards/spdx]]

## 與既有知識的關係
- 支持：[[sources/2026-10-01-anchore-oss-overview]]
- 矛盾：無
- 新增：支援生態系與輸出格式清單、attestation 能力

## 待追問題
- 對 .NET 的偵測方式與精確度（見 [[practices/dotnet-sbom-syft-grype]] 實測）。
