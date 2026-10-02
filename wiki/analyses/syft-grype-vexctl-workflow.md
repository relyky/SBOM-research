---
title: syft → grype → vexctl 使用順序
type: analysis
tags: [sbom, analysis, syft, grype, vexctl, vex]
aliases: [SBOM 工具鏈流程]
sources: [raw/tools/Syft.md, raw/tools/Grype.md, raw/tools/vexctl.md]
question: syft、grype、vexctl 三個工具的使用順序為何？
created: 2026-10-02
updated: 2026-10-02
status: draft
---

# syft → grype → vexctl 使用順序

## 問題

三個工具如何串接成「產生 SBOM → 掃描漏洞 → 聲明可利用性」的流程？

## 結論（TL;DR）

[[tools/syft-grype|syft]] 產生 SBOM，[[tools/syft-grype|grype]] 以 SBOM 掃描漏洞，經人工研判後用 [[tools/vexctl|vexctl]] 寫 [[concepts/vex|VEX]]，再讓 grype 帶 VEX 重掃。[^g][^v]

## 分析

```mermaid
flowchart TD
    A([開始：映像檔 / 目錄 / 原始碼]) --> B["syft：產生 SBOM<br/>syft &lt;target&gt; -o cyclonedx-json=sbom.cdx.json"]
    B --> C["grype：以 SBOM 掃描漏洞<br/>grype sbom:sbom.cdx.json -o json"]
    C --> D{有發現漏洞？}
    D -- 否 --> Z([結束：交付 SBOM])
    D -- 是 --> E["人工研判每個 CVE<br/>是否真的可被利用？"]
    E --> F{可利用性判定}
    F -- affected --> G["修補：升級 / 換元件"]
    G --> A2["重新建置"] --> B
    F -- "not_affected / fixed /<br/>under_investigation" --> H["vexctl create：建立 OpenVEX 聲明<br/>--product --vuln --status --justification"]
    H --> I{有多份 VEX？}
    I -- 是 --> J["vexctl merge：合併 VEX 文件"]
    I -- 否 --> K
    J --> K["（選用）vexctl attest：簽章 VEX"]
    K --> L["grype 重掃並套用 VEX<br/>grype sbom:sbom.cdx.json --vex vex.openvex.json"]
    L --> M{剩餘漏洞需處理？}
    M -- 是 --> E
    M -- 否 --> N([結束：交付 SBOM + VEX])
```

分工：syft＝清單、grype＝比對漏洞、vexctl＝聲明漏洞對本產品是否有影響。
- grype 支援以 OpenVEX 過濾結果。[^g]（`--vex` 旗標的確切用法待驗證）
- vexctl 的 `filter` 目前僅支援 SARIF 掃描結果。[^v]

## 依據頁面
- [[tools/syft-grype]]
- [[tools/vexctl]]
- [[concepts/vex]]

## 限制與待補資料
- 流程圖為依工具職責整理的建議順序，grype `--vex` 實際參數與版本需求待實測（截至 2026-10）。
- 尚未有 grype 帶 VEX 重掃的實測紀錄。

[^g]: [[sources/2026-10-01-anchore-grype-readme]]
[^v]: [[sources/2026-10-02-openvex-vexctl-readme]]
