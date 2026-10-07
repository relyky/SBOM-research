---
title: SBOM 生命週期與 CI/CD 整合
type: practice
tags: [sbom, practice, ci-cd, vex, lifecycle]
sources: [wiki/analyses/sbom-practice-talk.marp.md]
created: 2026-10-07
updated: 2026-10-07
status: draft
---

# SBOM 生命週期與 CI/CD 整合

> 本頁內容主要為使用者簡報中的**作者建議**，非標準或法規要求；工具指令多取自 README、未實測。[^s]

## 目標
讓 SBOM 不是一次性文件：每次建置重產，並隨弱點資料庫更新持續重掃。

## 適用情境
自家專案的 release build；已有 SBOM 的舊版本需定期複查。

## 流程步驟
1. **產生**：[[tools/syft-grype|syft]]、[[tools/cyclonedx-dotnet]]、[[tools/cyclonedx-npm]]、[[tools/retire-js]]。
2. **驗證**：[[tools/cyclonedx-cli]] validate、[[tools/sbom-tools]] validate。
3. **合併**：cyclonedx-cli merge（後端 + 前端）。
4. **掃描**：grype／[[tools/trivy]]（弱點 + 授權）。
5. **VEX 研判**：人工逐一判斷，以 [[tools/vexctl]] 或 trivy `--vex` 套用；見 [[concepts/vex]]。
6. **保存／發布**：命名見 [[practices/sbom-file-naming]]；簽章尚未做。[^s]

**兩個迴圈**：① 程式碼變更 → 重產 SBOM；② 弱點 DB 更新 → 對既有 SBOM 重掃（舊 SBOM 不必重產）。[^s]

## 角色與責任
未定（個人實踐）。

## 使用工具
見上列各步驟。

## CI/CD gate 建議（作者建議）
- 時機：每次 release build，與製品同流程（便於一併簽章）；另排程重掃既有版本。
- 擋：新增 Critical／High 弱點且無 VEX 聲明；授權不在核可清單；SBOM／VEX 格式驗證失敗。
- 留存：檔名 = 製品檔名 + `.cdx.json`；SBOM + 弱點報告 + 授權報告；工具版本與弱點 DB 建置時間。
- 指令範例（未實測）：`sbom-tools diff old new --fail-on-vex-gap`、`vexctl validate --strict`。[^s]

## 檢核清單
- 只掃要出貨的東西（publish 產物，或 `-ef`／`-t` 排除）
- 設定名稱與版本，檔名能對回製品
- 清點沒有 purl、沒有 license 的元件
- 檢查 retire 辨識結果並補登漏掉的函式庫
- 記錄工具版本與弱點 DB 建置時間；弱點報告留 table 與 JSON
- 高風險弱點逐一研判，結論寫成 VEX；排程重掃舊版本
- 腳本參數化後放進 CI

## 常見陷阱
掃錯範圍造成重複計算；「0 漏洞」被誤讀為安全；VEX 欄位拼錯會被讀取端默默丟棄。見 [[practices/dotnet-sbom-syft-grype]]、[[concepts/vex]]。

## 業界案例
（尚無）

## 參考來源
[^s]: [[analyses/sbom-practice-talk.marp|簡報：SBOM 實戰分享]]（使用者自製，本庫衍生品）
