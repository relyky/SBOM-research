---
title: vexctl
type: tool
tags: [sbom, tool, vex, openvex, sigstore]
sources: [raw/tools/vexctl.md]
vendor: OpenVEX 專案
license: 來源未標示
version_checked: 未標示（README 提及 OpenVEX v0.2.0、cosign v3；截至 2026-10 剪藏）
created: 2026-10-02
updated: 2026-10-02
status: stub
---

# vexctl

> 本頁僅依官方 README 撰寫，尚無實測。

## 用途與定位
建立、合併、驗證、簽證 [[concepts/vex|VEX]] 文件（OpenVEX），並將其套用到掃描結果以濾除不可利用的弱點。[^s]

## 支援範圍
- 輸出格式：OpenVEX（v0.2.0）；簽證輸出為 sigstore bundle 或 DSSE envelope[^s]
- 語言/生態系：不限；以 purl 識別產品，範例含 apk 套件與容器映像[^s]
- 輸入來源：命令列參數、golden file 規則、既有 VEX 文件、容器映像上的 attestation、SARIF 掃描結果[^s]

## 基本用法
```bash
# 建立
vexctl create --product="pkg:apk/wolfi/git@2.38.1-r0?arch=x86_64" \
  --vuln="CVE-2014-123456" --status="not_affected" \
  --justification="inline_mitigations_already_exist"

# 合併、驗證（CI 建議 --strict）
vexctl merge --product=pkg:apk/wolfi/bash@1.0.0 a.vex.json b.vex.json
vexctl validate --strict .openvex/*.json

# 簽證並附加到映像
vexctl attest --attach --sign mydata.vex.json cgr.dev/image@sha256:...

# 以 VEX 過濾 SARIF
vexctl filter scan_results.sarif.json vex_data.csaf
```
（命令取自來源[^s]，尚未實測）

## CI/CD 整合
`validate` 有錯誤即回傳非零 exit code，`--strict` 連警告也失敗，來源建議用於 CI。[^s]

## 優缺點
- 優：一個工具涵蓋建立、驗證、簽證、過濾；多份文件依時間重播，可表達 `under_investigation` → `not_affected` 的演進。[^s]
- 缺：`filter` 目前僅支援 SARIF；`validate` 只檢查 OpenVEX v0.2.0，舊版文件需經 `merge` 改寫。[^s]

## 實測紀錄
（尚無）

## 參考來源
[^s]: [[sources/2026-10-02-openvex-vexctl-readme]]
