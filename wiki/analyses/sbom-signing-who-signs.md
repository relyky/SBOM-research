---
title: SBOM 簽章：誰來簽、簽什麼
type: analysis
tags: [sbom, analysis, signing, provenance, attestation, integrity]
aliases: [誰來簽章, SBOM signing]
sources: [raw/industry/Software supply chain.md, raw/industry/Types of Software Bill of Material (SBOM) Documents.md, raw/tools/CycloneDX CLI tool for SBOM.md, raw/tools/vexctl.md, raw/tools/Syft.md, raw/tools/cyclonedx-npm.md]
question: 「可見性 ≠ 完整性：SBOM 只說有什麼；要證明沒被竄改，還需要 provenance 與簽章」——簽章由誰簽？是行政面負責人的簽署，還是工具面的簽章？簽的對象是程式碼元件，還是具法律效力的聲明？
created: 2026-11-03
updated: 2026-11-03
status: draft
---

# SBOM 簽章：誰來簽、簽什麼

## 問題

[[analyses/sbom-practice-talk.marp|簡報]]中有一句：「**可見性 ≠ 完整性**：SBOM 只說『有什麼』；要證明沒被竄改，還需要 provenance 與簽章。」這裡的「簽章」由誰來簽？屬於行政面（負責人簽署），還是工具面？簽的對象是元件（程式碼），還是具法律效力的正式聲明？

## 結論（TL;DR）

- 這裡的簽章是**工具面的數位簽章**（digital signature），以密碼學方式由工具或 CI 執行，簽的是**數位檔案**（SBOM、製品或 attestation），不是紙本，也不是法律聲明。
- **誰對內容負責，誰就簽**：通常是軟體供應者，最好由**建置流程（CI 身分）**來簽，而不是工程師個人。金鑰或身分屬於組織，因此代表「這是 A 公司發出的」，但這只是技術上的來源歸屬，不是個人的法律擔保。
- 簽章證明「**誰說的、說完有沒有被改**」，**不證明內容正確、完整或安全**。
- 行政或法律面的負責人簽署是**另外一份文件**，例如 CISA 安全軟體開發自我證明表、歐盟 CRA 符合性聲明（待驗證）。

## 分析

### 1. 簽章能證明與不能證明的事

| 能證明 | 不能證明 |
|---|---|
| 文件出自持有金鑰／身分者（來源真實性） | 內容正確或完整：漏列元件的 SBOM 簽了仍是漏列 |
| 簽完後內容未被竄改（完整性） | 製品本身安全 |

SBOM 與 provenance 提供可見性，但可見性本身不保證完整性；簽章式 attestation 可記錄製品來源、所用原始碼與依賴及建置步驟（例：in-toto）。[^ssc] 換句話說，三者各管一件事：SBOM 說「有什麼」，provenance 說「怎麼建的」，簽章說「誰說的、有沒有被改」。

### 2. 不同對象，簽的人不同

| 簽什麼 | 誰簽 | 說明 |
|---|---|---|
| 製品（exe、映像、套件） | 供應者的建置流程 | 傳統 code signing（待驗證） |
| SBOM | 產生 SBOM 的一方 | Build SBOM 可與製品由同一建置流程簽章 [^types] |
| Provenance | 建置平台本身 | SLSA 較高等級要求由建置平台產生並簽 provenance，避免自己證明自己（待驗證） |
| VEX | 做出可利用性判斷者（供應者 PSIRT） | `vexctl attest --attach --sign` 將 VEX 以 sigstore bundle 附加到映像 [^vexctl] |
| 第三方 Analyzed SBOM | 做分析的第三方 | 只代表第三方的分析結果，不代表原廠背書（待驗證） |

清單中第三方元件本身不由你簽，而是由各自維護者簽（如 NuGet 套件簽章、npm provenance）（待驗證）。

### 3. 金鑰模式：真正的難題是金鑰交給誰

**A. 長期金鑰**
- 例：[[tools/cyclonedx-cli]] 以 `keygen` 產生 RSA 金鑰對（PEM），`sign bom`／`sign file`（PKCS1 RSA SHA256），`verify all`／`verify file` 驗簽。[^cdxcli]
- 難題：私鑰保管位置（CI secret、KMS／HSM）、存取權限、外洩撤銷、公鑰如何可信地交付客戶。（待驗證）

**B. Keyless（Sigstore／cosign）**（待驗證）
- CI 以 OIDC 身分（如特定 repo 的 GitHub Actions workflow）向 Fulcio 換短效憑證，簽完即丟；簽章紀錄寫入 Rekor 透明日誌。
- 驗證者檢查的是「簽章身分是否為預期的 workflow」，而非公鑰。

### 4. 簽章要綁定製品

只簽 SBOM 檔，只能證明這份 JSON 沒被改，不能證明它描述的就是手上那個製品。in-toto attestation 把製品 hash 寫進 `subject`，讓簽章同時綁住「SBOM 內容」與「哪個製品」（待驗證）。[[tools/syft-grype|Syft]] 可用 in-toto 規格建立簽章的 SBOM attestation。[^syft]

### 5. 工具面簽章 vs. 行政面簽署

| | SBOM／製品簽章 | 合規聲明簽署 |
|---|---|---|
| 性質 | 工具面、密碼學 | 行政面、法律 |
| 簽署者 | CI 或工具，代表組織身分 | 負責人（如執行長或其指定人） |
| 對象 | 數位檔案（SBOM、製品、attestation） | 聲明文件 |
| 證明 | 來源與未被竄改 | 組織承諾遵循特定要求 |
| 例 | cosign、cyclonedx-cli sign、vexctl attest | CISA Secure Software Development Attestation Form、歐盟 CRA 符合性聲明（Declaration of Conformity）（待驗證） |

簡報那句話指的是**工具面**的數位簽章；為避免誤解，可改寫為「數位簽章」。

### 6. 落地建議（自身環境）

[[practices/sbom-lifecycle-and-ci]] 目前「簽章尚未做」。可行做法（本庫建議，未實測）：
- 簽章人：公司（供應者），由 release build 的 CI job 執行，不在個人電腦上簽。
- 有 GitHub Actions：cosign keyless，客戶驗證 workflow 身分。
- 地端或無 OIDC：cosign 或 cyclonedx-cli 搭配 KMS 保管金鑰，私鑰只給 CI 使用。
- [[tools/cyclonedx-npm]] 的產出「幾乎」符合 OWASP SCVS Level-2，僅簽章需外部完成，可由上述流程補上。[^npm]
- 客戶端需先取得「預期的簽章身分或公鑰」，否則驗章無意義。

## 依據頁面
- [[concepts/software-supply-chain]]
- [[concepts/sbom]]
- [[concepts/sbom-types]]
- [[tools/cyclonedx-cli]]
- [[tools/vexctl]]
- [[tools/syft-grype]]
- [[tools/cyclonedx-npm]]
- [[practices/sbom-lifecycle-and-ci]]
- [[analyses/sbom-practice-talk.marp]]

## 限制與待補資料
- 大量內容（Sigstore keyless 機制、SLSA provenance 等級、in-toto `subject`、套件生態系簽章）為背景知識，標示「待驗證」；建議 ingest：SLSA spec、Sigstore 文件、in-toto attestation spec。
- EO 14028、NTIA、CISA、歐盟 CRA 是否**強制**要求 SBOM 簽章，本庫尚無法規原文佐證。
- 行政面簽署（CISA Secure Software Development Attestation Form、CRA 符合性聲明）尚無原文來源。
- [[tools/cyclonedx-cli]] 的簽章為 BOM 內嵌（JSF）或外部檔、與 Sigstore 路線的關係，仍待釐清。

[^ssc]: [[sources/2026-10-01-wikipedia-software-supply-chain]]
[^types]: [[sources/2026-10-01-openssf-sbom-types]]
[^vexctl]: [[sources/2026-10-02-openvex-vexctl-readme]]
[^cdxcli]: [[sources/2026-10-06-cyclonedx-cli-readme]]
[^syft]: [[sources/2026-10-01-anchore-syft-readme]]
[^npm]: [[sources/2026-10-07-cyclonedx-npm-readme]]
