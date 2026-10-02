---
title: openvex/vexctl README
type: source
tags: [sbom, vex, openvex, tool, sigstore]
sources: [raw/tools/vexctl.md]
source_url: https://github.com/openvex/vexctl
source_author: OpenVEX 專案
source_date: 未標示（剪藏於 2026-10-02；內文範例時間為 2023，並提及 OpenVEX v0.2.0）
created: 2026-10-02
updated: 2026-10-02
status: draft
---

# openvex/vexctl README

## 基本資訊
- 類型：工具文件（官方 README）
- 作者/發布者：OpenVEX 專案（github.com/openvex）
- 發布日期：未標示
- 可信度評估：官方一手（工具行為）；非 OpenVEX 規格本身

## 重點摘要
1. 定位：建立、套用、簽證 VEX 資料的 CLI，目的是「關掉」已知不影響產品的掃描器警示；README 將 VEX 比喻為「負面安全公告（negative security advisory）」。[^s]
2. 三種運作模式：建立 VEX 文件（`create`／`merge`／`validate`）、包成簽章 attestation（`attest`）、套用到掃描結果（`filter`）。[^s]
3. `vexctl create` 以 `--product`（purl）、`--vuln`、`--status`、`--justification` 產生 OpenVEX 文件；來源也可是「golden file」預定義規則或合併既有文件。[^s]
4. `vexctl merge` 合併多個發布者的文件，依時間排序「重播」狀態；範例為 `under_investigation` 四小時後變 `fixed`。[^s]
5. `vexctl validate` 檢查文件是否符合 OpenVEX v0.2.0：錯誤（error）代表違規，警告（warning）代表可解析但含被忽略／冗餘資料；有錯誤時回傳非零 exit code，`--strict` 讓警告也失敗（建議用於 CI），`--format=json` 輸出機器可讀結果。[^s]
6. `vexctl attest --attach --sign` 將 VEX 以 sigstore bundle 附加到容器映像（OCI referrers API，cosign v3 版面）；`--format dsse` 輸出裸 DSSE envelope，`--attach-method legacy` 用舊的 cosign `.att` tag 版面。[^s]
7. `vexctl filter <SARIF 檔> <VEX 檔或映像>` 從掃描結果移除 VEX 標為不可利用的項目；目前僅支援 SARIF，專有格式為規劃中。VEX 來源範例含 `.csaf` 檔與映像上的 attestation。[^s]
8. 安裝：預建簽章執行檔（可用 cosign 驗證）、`brew install vexctl`、`go install github.com/openvex/vexctl@latest`。[^s]

## 關鍵主張與數據
- 「VEX can be thought of as a "negative security advisory".」— 意涵：VEX 是撤銷／降級警示的來源，而非新增警示。
- 「readers are forgiving — vexctl, like most consumers, ignores data it does not recognize, so a misspelled field name is not rejected but quietly dropped」— 意涵：VEX 文件需在產出端驗證，否則欄位拼錯會讓聲明悄悄失效。
- 「either justification or impact statement must be defined when using status "not_affected"」— 意涵：OpenVEX 中 `not_affected` 必須附理由。
- 範例文件 `@context` 為 `https://openvex.dev/ns/v0.2.0`，statement 含 `vulnerability`、`products[@id]`（purl）、`status`、`justification`、`timestamp`。

## 影響的 wiki 頁面
- [[tools/vexctl]] — 新建
- [[concepts/vex]] — 補 OpenVEX 結構、狀態值、justification、驗證與簽證、多文件合併
- [[overview]]、[[index]]

## 與既有知識的關係
- 支持：[[sources/2026-10-01-aqua-what-is-vex]] 所述 OpenVEX 為三種 VEX 實作之一；[[sources/2026-10-01-anchore-grype-readme]] 稱 Grype 支援 OpenVEX。
- 矛盾：無。注意詞彙差異：CycloneDX VEX 範例用 `code_not_reachable`，OpenVEX 用 `vulnerable_code_not_in_execute_path`，兩者為不同格式各自的詞彙，不視為矛盾。
- 新增：OpenVEX 狀態值（`not_affected`／`under_investigation`／`fixed`）與驗證規則的一手說明；VEX 以 sigstore 簽證並附加到容器映像的做法；`filter` 以 SARIF 為介面。

## 待追問題
- OpenVEX 規格本身（`affected` 狀態、完整 justification 清單）尚無一手來源。
- Trivy／Grype 套用 OpenVEX 的實際行為與 vexctl `filter` 是否一致？
- 是否值得在 .NET 實測中加入 VEX 流程（syft → grype → vexctl）？

[^s]: raw/tools/vexctl.md
