---
title: Anchore OSS：開源工具總覽（Syft／Grype／Grant）
type: source
tags: [sbom, tool, anchore]
sources: [raw/tools/Overview of Anchore Open Source tools.md, raw/assets/Anchore tools flow.png]
source_url: https://oss.anchore.com/docs/projects/
source_author: Anchore
source_date: 2026-09-29（頁面最後修改）
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# Anchore OSS：開源工具總覽

## 基本資訊
- 類型：工具文件（官方）
- 作者/發布者：[[organizations/anchore|Anchore]]
- 發布日期：頁面最後修改 2026-09-29
- 可信度評估：官方一手（廠商自述）

## 重點摘要
1. Anchore 維護三個命令列工具：Syft（SBOM 產生）、Grype（弱點掃描）、Grant（授權掃描）；多為 Go 撰寫，皆為 Apache-2.0。
2. 工作流程：用 Syft 產生一次 SBOM 作為證據，再由 Grype 掃弱點、Grant 掃授權合規，各自獨立。
3. 附圖（`raw/assets/Anchore tools flow.png`）：Your Software（容器映像、檔案系統、封存檔）→ scan → Syft → generates → SBOM → analyze → Grype → Security Report（CVE findings）／Grant → License Report（Compliance info）。

## 關鍵主張與數據
- 「This modular approach lets you generate the SBOM once with Syft, then use Grype and Grant independently to scan for different types of risk.」— 意涵：SBOM 是共用中介物，產生與消費解耦。

## 影響的 wiki 頁面
- [[tools/syft-grype]] — 由 stub 補成 draft，並納入 Grant
- [[organizations/anchore]] — 新建
- [[concepts/sbom]] — 補充「產生一次、多處消費」

## 與既有知識的關係
- 支持：[[sources/2026-10-01-moea-sbom-trends]] 對 Syft、Grype 的簡述（二手說法獲一手驗證）
- 矛盾：無
- 新增：Grant 授權掃描工具

## 待追問題
- Grant 的實際用法與政策格式（尚無來源）。
