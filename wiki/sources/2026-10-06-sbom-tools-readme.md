---
title: sbom-tool/sbom-tools README
type: source
tags: [sbom, tool, cyclonedx, spdx, compliance]
sources: [raw/tools/sbom-tools.md]
source_url: https://github.com/sbom-tool/sbom-tools
source_author: sbom-tool GitHub 組織（維護者未載明）
source_date: 未載明（剪藏日 2026-10-06；範例提及 v0.1.19）
created: 2026-10-06
updated: 2026-10-06
status: draft
---

# sbom-tool/sbom-tools README

> 注意：此工具（`sbom-tool/sbom-tools`，Rust）與 Microsoft 的 `microsoft/sbom-tool`（見 [[tools/microsoft-sbom-tool]]）是不同專案，名稱極易混淆。

## 基本資訊
- 類型：工具文件
- 作者/發布者：`sbom-tool` GitHub 組織（與 CycloneDX、OWASP、Microsoft 的關係未載明）
- 發布日期：未載明；剪藏日 2026-10-06
- 可信度評估：官方一手（工具 README），但其對法規版本的描述屬工具方轉述，非法規原文

## 重點摘要
1. 把 CycloneDX（1.4–1.7）與 SPDX（2.2–2.3、3.0）轉成單一正規化模型，用同一 Rust 引擎做語意 diff、驗證、品質評分、補強與報告；另提供 Go／Swift／Python／Node.js 綁定（MVP）。
2. 指令：`diff`、`view`、`validate`、`quality`、`query`、`diff-multi`、`timeline`、`matrix`、`enrich`、`convert`、`license-check`；預設 TTY 開 TUI。
3. 合規驗證含 16 種標準（NTIA、CISA 2026、FDA、CRA、SSDF、EO 14028、BSI TR-03183-2、EUCC、EU AI Act、PCI DSS 6.3.2、CISA FSCT 等），輸出 SARIF／OSCAL 等。
4. 以 OSV、KEV 補強漏洞資訊，並可疊加 OpenVEX；`--fail-on-vex-gap` 等旗標提供 CI 閘門，結束碼 0–7 各有定義。
5. 品質評分 0–100（9 種 profile），並可輸出 sbomqs 相容 JSON；兩種分數不可互換。
6. 支援 CBOM（密碼學清單）與 AI-BOM；含 CNSA 2.0、NIST IR 8547 後量子密碼檢查。
7. 可由 stdin 讀入（`syft -o cyclonedx-json . | sbom-tools quality -`、`cosign download sbom ... | sbom-tools validate -`）；輸入上限 512 MB；`--offline` 模式。
8. 安裝：Homebrew、預編譯二進位（Sigstore 簽章與 GitHub attestation）、cargo；從原始碼建置需 Rust 1.88+。

## 關鍵主張與數據
- 「`cisa-2026` — CISA/NSA/FBI *2026 Minimum Elements for an SBOM* (v2.1, 2026-07-29), the successor to NTIA 2021 and deliberately stricter」— 意涵：NTIA 2021 最低要素已有後繼版本（僅此工具 README 轉述，待 CISA 原文）。
- 「a tool-only creator list does not satisfy SBOM Author, and silently omitting a license fails where an explicit `NOASSERTION` passes.」— 意涵：新版對 SBOM 作者與授權欄位更嚴格。
- 「A passing verdict is evidence that the inventory exists and is usable — **not** a PCI DSS compliance certification.」— 意涵：工具通過 ≠ 合規認證。
- 「**Structural verification only** — signature *presence* is recorded, never cryptographically verified」（CDXA 證明）— 意涵：不驗證證明的簽章。
- 「Until 1.0 a breaking change may land in a minor release」— 意涵：JSON 輸出契約尚未穩定，宜鎖定版本。

## 影響的 wiki 頁面
- [[tools/sbom-tools]] — 新增
- [[regulations/ntia-minimum-elements]] — 補 CISA 2026 後繼版本（待驗證）
- [[concepts/vex]]、[[standards/cyclonedx]]、[[standards/spdx]]、[[overview]]、[[index]]

## 與既有知識的關係
- 支持：[[concepts/vex]] 的 OpenVEX 流程（可疊加 OpenVEX 文件）；[[concepts/purl]] 為其比對的第一層鍵。
- 矛盾：與 [[regulations/ntia-minimum-elements]] 並無衝突，但該頁未提 NTIA 2021 已有後繼版本，已加註。
- 新增：品質評分、法規閘門、跨版本語意 diff、機群查詢（「哪裡有 log4j」）等「消費端」能力。

## 待追問題
- 維護者與成熟度（範例版本 v0.1.19，屬 1.0 前）？
- CISA 2026 Minimum Elements v2.1 的原文與 EU CRA 條文需另蒐集核對。
- 與 sbomqs、Dependency-Track 的功能差異？
