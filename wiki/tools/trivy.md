---
title: Trivy
type: tool
tags: [sbom, tool, vex, scanner]
sources: [raw/industry/What Is VEX(Vulnerability Exploitability eXchange).md]
vendor: Aqua Security
license: 開源（具體授權待驗證）
version_checked: 未查證（來源為 2024-07 文章）
created: 2026-10-01
updated: 2026-10-01
status: stub
---

# Trivy

> 本頁僅依一份廠商文章撰寫，尚無實測。

## 用途與定位
開源的弱點與設定錯誤掃描工具，可產生 SBOM、以 SBOM 做弱點比對，並支援以 VEX 過濾結果。[^a] Aqua 稱 Trivy 是最早支援 VEX 的掃描器之一。[^a]

## 支援範圍
- 輸出格式：CycloneDX（來源範例）；其他格式待驗證
- 語言/生態系：來源範例為容器映像（Debian）；其他待驗證
- 輸入來源：容器映像、SBOM 檔

## 基本用法
```bash
# 產生 SBOM
trivy image --format cyclonedx --output debian11.sbom.cdx debian:11

# 以 SBOM 掃描並套用 VEX
trivy sbom debian11.sbom.cdx --vex trivy.vex.cdx
```
（命令取自來源[^a]，尚未實測）

## CI/CD 整合
待補。

## 優缺點
- 優：可串起「產生 SBOM → 掃描 → 以 VEX 去除不可利用弱點」流程。[^a]
- 缺：來源為廠商文章，無獨立評估。

## 實測紀錄
（尚無）

## 參考來源
[^a]: [[sources/2026-10-01-aqua-what-is-vex]]
