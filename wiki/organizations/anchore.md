---
title: Anchore
type: organization
tags: [sbom, anchore, vendor]
aliases: [Anchore Inc.]
sources: [raw/tools/Overview of Anchore Open Source tools.md, raw/tools/Syft.md, raw/industry/軟體物料清單SBOM發展趨勢.md]
created: 2026-10-01
updated: 2026-10-01
status: stub
---

# Anchore

## 定義
SBOM 與軟體供應鏈安全廠商，贊助並維護 Syft、Grype、Grant 等開源工具。[^o][^s]

## 為什麼重要
其工具是 CycloneDX／SPDX 格式 SBOM 的主流開源產生與掃描方案之一；資策會文章將其列為資服業者代表。[^m]

## 在 SBOM 生態中的角色
- 維護 [[tools/syft-grype|Syft、Grype、Grant]]，皆為 Apache-2.0。[^o]
- 提供商業支援（需另行聯繫）。[^s]
- 開源專案定期舉辦社群會議。[^s]

## 主要產出
- [[tools/syft-grype]]

## 實務注意事項
商業版功能與開源差異：尚無來源。

## 開放問題
- 與 Aqua（[[tools/trivy|Trivy]]）的功能比較：待取得 Trivy 一手文件後做 `analyses/`。

## 參考來源
[^o]: [[sources/2026-10-01-anchore-oss-overview]]
[^s]: [[sources/2026-10-01-anchore-syft-readme]]
[^m]: [[sources/2026-10-01-moea-sbom-trends]]
