---
title: purl（Package URL）
type: concept
tags: [sbom, concept, component-identification]
aliases: [purl, Package URL, pkg URL]
sources: [raw/tools/vexctl.md, raw/tools/syft-grype.sample.md, raw/assets/publish.sbom.cdx.json, raw/tools/cyclonedx-npm.md]
created: 2026-10-02
updated: 2026-10-07
status: stub
---

# purl（Package URL）

> stub：本庫尚無 purl 規格一手來源，內容僅來自工具文件與實測輸出；規格細節標示（待驗證）。

## 定義
以 `pkg:` 開頭的字串，用來識別一個軟體套件（類型、名稱、版本）。實測 SBOM 內的例子：`pkg:nuget/AspectInjector@2.9.0`；vexctl 範例為 `pkg:apk/wolfi/git@2.38.1-r0?arch=x86_64`。[^p][^v]

## 為什麼重要
- 漏洞比對的鍵：Grype 只能比對有 purl 的套件，無 purl 的元件不在掃描範圍，因此「0 漏洞」不等於無風險。[^s]
- [[concepts/vex|VEX]] 的產品識別：OpenVEX 以 purl 作為 `products[@id]`，`vexctl create --product` 也接受 purl。[^v]
- 在 [[standards/cyclonedx|CycloneDX]] 中是各元件的 `purl` 欄位，與 `cpe` 並列。[^p]

## 運作方式 / 細節
- 字串結構為 `pkg:<type>/<namespace>/<name>@<version>?<qualifiers>#<subpath>`；`type` 對應生態系（如 `nuget`、`apk`）。（待驗證，本庫僅見到 `type`、`name`、`version`、`?arch=` 的實例）
- 空白等特殊字元需百分比編碼，如 `pkg:nuget/Aspect%20Injector@2.9.0.0`。[^p]
- 驗證：`vexctl validate` 會檢查 purl，缺少 type 或 name 時回報錯誤（如 `pkg:not a purl`）。[^v]

## 相關概念
- [[concepts/sbom|SBOM]] — purl 是元件識別欄位
- [[concepts/vex|VEX]] — 以 purl 指定受影響產品
- [[concepts/cve|CVE]] — 弱點端識別碼，與 purl 配對比對
- [[standards/swid|SWID]] — 另一種軟體識別方式（以標籤檔識別已安裝軟體）

## 實務注意事項
- .NET 專案：`dotnet-sbom-syft-grype` 流程建議檢查 SBOM 元件是否皆有 purl，並清點無 purl 者；實測 176 個元件中 6 個 `application` 元件無 purl。見 [[practices/dotnet-sbom-syft-grype]]。[^s]
- [[tools/cyclonedx-npm]] 的 `--short-PURLs` 會移除所有 qualifier，換取較短字串；README 明言「causes information loss」。[^n]
- 同一套件可能出現名稱寫法不同的多筆 purl（實測有 `Aspect Injector` 與 `AspectInjector` 兩筆）。[^p]

## 開放問題
- purl 規格全文與治理單位（待補一手來源）。
- purl 與 CPE 並存時，各掃描器的比對優先順序與誤報差異。
- 無 purl 的元件如何人工補登。

## 參考來源
[^p]: raw/assets/publish.sbom.cdx.json
[^s]: [[sources/2026-10-01-syft-grype-dotnet-sample]]
[^v]: [[sources/2026-10-02-openvex-vexctl-readme]]
[^n]: [[sources/2026-10-07-cyclonedx-npm-readme]]
