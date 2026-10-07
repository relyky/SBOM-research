---
marp: true
type: analysis
tags: [sbom, analysis, slides, marp]
sources: [wiki/practices/sbom-lifecycle-and-ci.md, wiki/practices/dotnet-sbom-syft-grype.md, wiki/practices/dotnet-sbom-cyclonedx-trivy.md]
question: 如何向有經驗的工程師分享 SBOM 概念、流程與 .NET 落地經驗？
created: 2026-10-07
updated: 2026-10-07
status: draft
lang: zh-TW
title: SBOM 實戰：從看得到元件，到知道真正的風險
author: John
paginate: true
size: 16:9
footer: SBOM 實戰分享
style: |
  :root {
    --petrol: #0F3B3A;
    --teal: #0E7C6B;
    --amber: #E8A33D;
    --red: #C8424F;
    --slate: #3D5A80;
    --sage: #8CC5B6;
    --gray: #5C6B73;
    --tint: #EDF3F1;
    --ink: #1B2A2F;
  }
  section {
    font-family: "Microsoft JhengHei", "Noto Sans CJK TC", "PingFang TC", Calibri, sans-serif;
    font-size: 26px;
    color: var(--ink);
    background: #FFFFFF;
    padding: 50px 64px 60px;
    justify-content: flex-start;
  }
  h1 { font-size: 40px; color: var(--petrol); margin: 0 0 20px; }
  h2 { font-size: 28px; color: var(--teal); margin: 12px 0 8px; }
  h3 { font-size: 24px; color: var(--petrol); margin: 10px 0 6px; }
  strong { color: var(--teal); }
  em { color: var(--gray); }
  ul, ol { margin: 4px 0; }
  li { margin: 4px 0; }
  table { font-size: 20px; border-collapse: collapse; margin: 8px 0; }
  th { background: var(--petrol); color: #fff; }
  th, td { border: 1px solid #C9D6D2; padding: 6px 12px; }
  tr:nth-child(even) td { background: var(--tint); }
  pre { background: var(--petrol); color: #E6F0EE; border-radius: 10px; padding: 14px 18px; font-size: 17px; line-height: 1.35; }
  pre code { background: transparent; color: inherit; }
  pre code, pre code * { color: #E6F0EE !important; font-weight: normal !important; }
  pre code .hljs-string, pre code .hljs-number { color: #F2C879 !important; }
  pre code .hljs-comment { color: #8CC5B6 !important; font-style: italic; }
  pre code .hljs-attr, pre code .hljs-keyword, pre code .hljs-built_in { color: #A9D8F5 !important; }
  td:first-child { white-space: nowrap; }
  code { font-family: "Courier New", Consolas, monospace; background: var(--tint); color: var(--petrol); padding: 0 4px; border-radius: 4px; }
  blockquote { border-left: none; background: var(--tint); border-radius: 10px; padding: 12px 18px; margin: 12px 0; color: var(--ink); font-size: 21px; }
  footer { color: var(--gray); font-size: 14px; }
  section::after { color: var(--gray); font-size: 14px; }
  .hl { color: var(--red); }
  section.lead, section.dark {
    background: var(--petrol);
    color: #FFFFFF;
  }
  section.lead { justify-content: center; }
  section.lead h1, section.dark h1 { color: #FFFFFF; font-size: 52px; }
  section.dark h1 { font-size: 40px; }
  section.lead h2, section.dark h2 { color: var(--amber); }
  section.lead p, section.dark p, section.lead li, section.dark li { color: var(--sage); }
  section.lead strong, section.dark strong { color: var(--amber); }
  section.lead code, section.dark code { background: #1C5553; color: #FFFFFF; }
  section.lead footer, section.dark footer { color: var(--sage); }
  section.lead::after, section.dark::after { color: var(--sage); }
  section.divider h2 { font-size: 96px; margin: 0; color: var(--amber); }
  section.small { font-size: 22px; }
  section.small pre { font-size: 15px; }
  section.small table { font-size: 18px; }
---

<!-- _class: lead -->
<!-- _paginate: false -->
<!-- _footer: "" -->

# SBOM 實戰：從看得到元件，到知道真正的風險

軟體物料清單（Software Bill of Materials）的概念、流程與 .NET 落地經驗

John ・ 2026-10

<!--
開場自我介紹。這份分享整理自我這陣子研究 SBOM 的知識庫和實際在 .NET 專案上的實驗。聽眾都是有經驗的工程師，所以會少講定義、多講指令、資料格式和踩過的坑。
-->

---

# 先問一個問題

**2021-12 ・ Log4Shell 爆發那天**

## 你能在 1 小時內回答：「我們有哪些系統用了 log4j < 2.17.0？」

如果每個版本都留有 SBOM，答案只是一行查詢：

```bash
sbom-tools query "log4j" --version "<2.17.0" fleet/*.json
```

*沒有 SBOM：逐一翻 repo、問負責人、猜部署版本*

| 01 概念 | 02 流程 | 03 實務分享 |
|---|---|---|
| SBOM 是什麼、格式、識別碼、類型、VEX | 產生 → 驗證 → 掃描 → VEX → 保存，放進 CI/CD | .NET 兩條路線實測、前端 JS、踩坑與檢核清單 |

<!--
用 Log4Shell 當開場。那時很多團隊花了好幾天才確認哪些系統受影響。如果每個發佈版本都附帶 SBOM，這件事就變成查詢。sbom-tools 的 query 指令就是做這件事（指令取自其 README，尚未實測）。
-->

---

<!-- _class: lead divider -->
<!-- _paginate: false -->

## 01

# 概念

SBOM 是什麼、為什麼現在、格式與識別碼、六種類型、VEX

---

# SBOM：軟體的成分標示

**列出一個軟體由哪些元件組成**

- 名稱、版本、供應商、識別碼
- 元件之間的依賴關係
- 誰、在什麼時候產生這份清單
- 以機器可讀的標準格式交換

|  | lockfile | SCA 掃描報告 | SBOM |
|---|---|---|---|
| 目的 | 鎖定可重現的安裝版本 | 找出已知弱點 | 交換元件清冊 |
| 讀者 | 套件管理器 | 內部資安 | 客戶、稽核、下游、工具 |
| 格式 | 各生態系自訂 | 各廠商自訂 | SPDX／CycloneDX 標準 |
| 範圍 | 單一生態系 | 依工具而定 | 可跨生態系合併 |

> <span class="hl">**可見性 ≠ 完整性**</span>：SBOM 只說「有什麼」；要證明沒被竄改，還需要 provenance 與簽章。

<!--
SBOM 就像食品成分標示。比較表是我依概念整理的框架，不是某份標準的原文。另外強調：SBOM 是供應鏈透明度的基礎，但不是完整性保證。
-->

---

# 為什麼是現在：供應鏈攻擊推動了政策

| 時間 | 事件 | 說明 |
|---|---|---|
| 2014 | Heartbleed／Shellshock | 開源元件弱點波及全網 |
| 2017 | NotPetya | 經軟體更新擴散 |
| 2020-12 | SolarWinds | 惡意更新，逾 18,000 組織安裝 |
| 2021-05 | **EO 14028**（政策） | 要求提供 SBOM |
| 2021-07 | **NTIA 最低要素**（政策） | 定義 SBOM 基本欄位 |
| 2021-12 | Log4Shell | 大家都在問：我們有用嗎？ |
| 2024 | XZ Utils 後門 | 上游維護者被滲透 |

**96%** 商用程式碼庫含開源（Synopsys 2024）　**70–90%** 典型程式碼庫為開源元件（Linux Foundation 2022）

*來源：Wikipedia Software supply chain、資策會 MIC（二手資料）*

<!--
SolarWinds 之後美國在 2021-05-12 發布 EO 14028，要求 NTIA 在 60 天內定義 SBOM 基本元素，於 2021-07-12 發布。注意：這頁法規資訊來自二手來源，EO 14028 現行狀態尚未查證。
-->

---

<!-- _class: small -->

# 最低要素：SBOM 至少要有哪些欄位

三大類：**資料欄位**・自動化支援・實務與流程

1. 供應商名稱　2. 套件名稱　3. 套件版本　4. 其他唯一識別碼（如 purl）
5. 依賴關係　6. SBOM 作者　7. SBOM 產出時間

```jsonc
{
  "metadata": {
    "timestamp": "2026-10-01T08:00:00Z",          // 7
    "authors": [{ "name": "Build Team" }]         // 6
  },
  "components": [{
    "supplier": { "name": "..." },                // 1
    "name": "Newtonsoft.Json",                    // 2
    "version": "13.0.3",                          // 3
    "purl": "pkg:nuget/Newtonsoft.Json@13.0.3"    // 4
  }],
  "dependencies": [{ "ref": "...", "dependsOn": [...] }]   // 5
}
```

*NTIA 2021 版七項欄位對照 CycloneDX JSON（示意）。CISA 2026 後繼版據稱更嚴格，例如作者不能只寫工具、授權須明確標 NOASSERTION（待原文核對）。*

<!--
1–4 在 components，5 在 dependencies，6、7 在 metadata。CISA 2026 版的資訊只來自 sbom-tools README 的轉述，尚待原文核對。
-->

---

# 三種格式：工程實務多選 CycloneDX

| | SPDX | **CycloneDX** | SWID |
|---|---|---|---|
| 標準 | ISO/IEC 5962:2021 | ECMA-424（官方稱） | ISO/IEC 19770-2:2015 |
| 推動 | Linux Foundation | OWASP | NIST 推廣 |
| 定位 | 序列化格式最多：Tag:Value、JSON、XML、YAML、RDF | 專為 SBOM 設計，內建 VEX；涵蓋 10 類 BOM | 已安裝軟體標籤檔，偏資產管理 |
| 工具 | Microsoft sbom-tool 只輸出 SPDX 2.2／3.0 | 本次所有工具都能輸出 | 較少用在建置流程 |

> 需要 SPDX 時：`cyclonedx-cli convert` 可轉成 SPDX JSON 2.3，但官方明言**可能遺失資訊**。

<!--
SWID 由 ISO 定義、NIST 推廣，重點是端點上已安裝軟體的清冊。本次實務用到的工具都能輸出 CycloneDX，所以後面都以 CycloneDX JSON 為主。
-->

---

# 比對靠什麼：purl 對上 CVE

**purl（Package URL）：元件的身分證**

```text
pkg:nuget/Newtonsoft.Json@13.0.3
    └type └name           └version
```

完整結構還可帶 namespace、`?qualifiers`、`#subpath`；空白等字元需百分比編碼

**SBOM 元件**（每個帶 purl）→ **弱點資料庫**（OSV、GHSA、NVD）→ **CVE 編號**（MITRE 營運，CNA 分派）→ **VEX 研判**（對我是否可利用？）

> <span class="hl">**沒有 purl → 掃描器不會比對 → 「0 漏洞」不代表安全。**</span>
> 實測 SBOM 中 6 個 application 元件就沒有 purl。

<!--
grype 只比對有 purl 的套件，沒有 purl 的元件根本不在掃描範圍。purl 完整結構的細節本知識庫尚無規格一手來源。
-->

---

<!-- _class: small -->

# 六種 SBOM 類型：你掃出來的是哪一種？

| 類型 | 定義 | 特性 | 本次實務 |
|---|---|---|---|
| Design | 設計規格中預期的元件 | 可在購買授權前發現問題 | |
| **Source** | 由原始碼與依賴宣告產生 | 看得到依賴樹；可能含未出貨元件 | dotnet-CycloneDX、cyclonedx-npm |
| **Build** | 建置流程中產生 | 正確性較高；可與製品一起簽章 | （同上，放進建置流程） |
| **Analyzed** | 對建置產物做分析 | 不需原始碼；靠啟發式，可能遺漏 | syft dir:publish、retire.js |
| Deployed | 系統上已安裝軟體清冊 | 呈現實際安裝與設定 | |
| Runtime | 插樁記錄實際載入元件 | 看得到動態載入；需長時間執行 | |

*來源：CISA SBOM 類型文件（經 OpenSSF 轉載）；工具與類型的對照為本人推論*

<!--
同樣叫 SBOM，資料來源不同結果就不同。工具對類型的對照是我的推論。開源專案通常只負責 Source 與 Build。
-->

---

<!-- _class: small -->

# VEX：從「有幾個 CVE」到「有幾個真的能被利用」

**SBOM 說「我有什麼」；VEX 說「這個 CVE 對我有沒有影響」**

| 狀態 | 意義 |
|---|---|
| `not_affected` | 不受影響，必須附理由 |
| `affected` | 受影響，需修補 |
| `fixed` | 已修補 |
| `under_investigation` | 調查中，之後再更新 |

```json
{
  "@context": "https://openvex.dev/ns/v0.2.0",
  "statements": [{
    "vulnerability": { "name": "CVE-YYYY-NNNNN" },
    "products": [{ "@id": "pkg:nuget/Foo@1.2.3" }],
    "status": "not_affected",
    "justification": "vulnerable_code_not_in_execute_path"
  }]
}
```

*三種實作：OpenVEX、CSAF VEX、CycloneDX VEX。拼錯欄位會被讀取端默默丟棄，產出端要跑 `vexctl validate`。*

<!--
VEX 由 NTIA 在 2021 提出。不同格式的理由用詞不同：CycloneDX 用 code_not_reachable，OpenVEX 用 vulnerable_code_not_in_execute_path。CVE 編號是示意。
-->

---

<!-- _class: lead divider -->
<!-- _paginate: false -->

## 02

# 流程

SBOM 不是一次性文件：每次建置重產，弱點資料庫每天都在變

---

# 生命週期全景

| ① 產生 | ② 驗證 | ③ 合併 | ④ 掃描 | ⑤ VEX 研判 | ⑥ 保存／發布 |
|---|---|---|---|---|---|
| syft、dotnet-CycloneDX、cyclonedx-npm、retire.js | cyclonedx-cli validate、sbom-tools validate | cyclonedx-cli merge（後端 + 前端） | grype、trivy：弱點 + 授權 | vexctl、trivy --vex | 命名慣例、簽章、版本追蹤 |

> **兩個迴圈**
> ① 程式碼變更 → 重新產生 SBOM
> ② 弱點資料庫更新 → 對既有 SBOM 重掃
> 舊版本的 SBOM 不需要重產，但需要被重新掃描。

<!--
簽章在這次實務還沒做，列為下一步。
-->

---

<!-- _class: small -->

# 產生 SBOM 的兩種輸入

| | 從專案檔產生（偏 Source／Build） | 從建置產物分析（偏 Analyzed） |
|---|---|---|
| 工具 | `dotnet-CycloneDX`、`cyclonedx-npm`、`sbom-tool -bc` | `syft dir:publish`、`retire.js`、`trivy image` |
| 優點 | 有完整依賴樹；.NET 套件授權資訊較完整；可在建置前執行 | 貼近實際部署內容；抓得到 vendored 檔案；別人交付的產物也能掃 |
| 注意 | 可能含未出貨套件（用 `-ef`／`-t` 排除）；需要 dotnet restore 與網路 | 啟發式辨識，可能遺漏或錯誤；掃錯範圍會重複計算（1365 vs 176） |

<!--
我的建議：自家專案以專案檔為主，產物掃描做交叉驗證（兩者元件清單一致性尚未實測）。
-->

---

# 消費 SBOM：弱點與授權是兩件事

| | 弱點掃描 | 授權合規 |
|---|---|---|
| 比對鍵 | purl／CPE → 弱點資料庫 | 元件的 license 欄位 |
| 工具 | `grype sbom:<檔>`、`trivy sbom --scanners vuln` | `trivy sbom --scanners license` |
| 注意 | 資料庫要更新，並記錄建置時間 | syft 取不到 .NET 套件的授權資訊 |
| 產出／降噪 | 候選清單，還需要 VEX 研判 | 先排除 System.／Microsoft. 等前綴（可能誤排除同名前綴第三方） |

<!--
同一份 SBOM 明天掃的結果可能不同。syft 對 .NET 套件取不到授權資訊，是我換工具的原因。
-->

---

<!-- _class: small -->

# VEX 回饋迴圈：syft → grype → vexctl

```text
[1 syft 產生 SBOM] → [2 grype 掃描弱點] → [3 人工研判每個 CVE] → <4 可利用？>
                                                                   │
                     affected ─────────────────────────────────────┼──→ [5 升級／換元件，重建，回到 1]
                                                                   │
              not_affected／fixed／under_investigation             ▼
[交付 SBOM + VEX] ← [7 grype 套用 VEX 重新掃描] ← [6 vexctl create（可 merge／attest）]
                              │
                              └─ 剩餘弱點 → 回到 3
```

- 掃描結果為 0 時直接交付 SBOM
- 分工：syft = 清單、grype = 比對、vexctl = 聲明「這個弱點對本產品有沒有影響」
- 限制：vexctl filter 目前只吃 SARIF；grype 帶 VEX 重掃的參數與版本需求**尚未實測**

<!--
重點在第 3、4 步的人工研判：這一步沒有工具可以代勞。這張是流程設計，不是實測結果。
-->

---

<!-- _class: small -->

# 放進 CI/CD

**Build → 產生 SBOM → 掃描 → Gate → 保存／發布**

| 什麼時候跑 | 擋什麼（建議） | 留下什麼 |
|---|---|---|
| 每次 release build，與製品同一流程（便於一起簽章） | 新增 Critical／High 弱點且沒有 VEX 聲明 | 檔名 = 製品檔名 + `.cdx.json` |
| 排程重掃既有版本的 SBOM | 授權不在核可清單 | SBOM + 弱點報告 + 授權報告 |
| | SBOM 或 VEX 格式驗證失敗 | 工具版本、弱點 DB 建置時間 |

```bash
sbom-tools diff old.cdx.json new.cdx.json --fail-on-vex-gap   # 新弱點缺 VEX → exit 4
vexctl validate --strict vex.json                             # 警告也視為失敗
```

<!--
Gate 條件是我的建議，不是標準要求。指令取自工具 README，尚未實測。
-->

---

<!-- _class: lead divider -->
<!-- _paginate: false -->

## 03

# 實務分享

.NET 專案兩條路線的實測、前端 JS 補強，以及一路踩到的坑

---

<!-- _class: small -->

# 工具地圖

| 產生 | 驗證・合併・轉換 | 掃描 | VEX |
|---|---|---|---|
| ★ **syft**：多生態系；掃目錄／映像 | ★ **cyclonedx-cli**：validate／merge／diff／convert／sign | ★ **grype**：弱點；支援 OpenVEX | **vexctl**：create／merge／validate／attest |
| ★ **dotnet-CycloneDX**：.NET 專案檔；含授權 | **sbom-tools**：語意 diff、品質分數、16 種合規檢查 | ★ **trivy**：弱點 + 授權；--vex | **trivy --vex**：套用 VEX 過濾 |
| **cyclonedx-npm**：npm 依賴樹／lockfile | | ★ **retire.js**：JS 函式庫弱點 | |
| **Microsoft sbom-tool**：只輸出 SPDX | | | |
| ★ **retire.js**：前端 vendored JS | | | |

*★ 本次實測或腳本中使用。注意：Microsoft sbom-tool 與 sbom-tools（第三方 Rust 工具）是不同專案。*

---

<!-- _class: small -->

# 實驗一：syft + grype 掃 .NET 發佈產物

```bash
winget install Anchore.Syft
winget install Anchore.Grype

# 只掃 publish 產物，指定名稱與版本
syft dir:publish --source-name MyApp --source-version 1.7.14-release \
  -o cyclonedx-json=publish.sbom.cdx.json

grype db status
grype sbom:publish.sbom.cdx.json -o table
```

| 掃整個專案目錄 | 只掃 publish 產物 |
|---|---|
| <span class="hl">**1365**</span> 個元件（bin／obj／publish 重複計算） | **176** 個元件（170 個 NuGet + 6 個 application） |

- 掃描範圍決定清單品質：只掃要出貨的東西
- 設定 `--source-name`／`--source-version`；版本可從 `publish/*.deps.json` 取得

*實測環境：syft 1.52.0、grype 0.119.0、輸出 CycloneDX 1.7（2026-10-01）*

---

# 實驗一踩到的三個坑

### 1. 沒有 purl 就不會比對
grype 只比對有 purl 的套件；6 個 application 元件沒有 purl；同套件出現「Aspect Injector」與「AspectInjector」兩種寫法

### 2. 0 漏洞 ≠ 安全
matches 與 ignoredMatches 皆空 = 無「已知」弱點；.NET 執行環境本身不在掃描範圍；結果取決於 DB（本例 schema v6.1.9、built 2026-09-30）

### 3. 拿不到授權資訊
syft 取不到 .NET 套件的 license，無法快速檢查授權是否核可 → **這是改走 dotnet-CycloneDX 路線的主因**

---

<!-- _class: small -->

# 實驗二：dotnet-CycloneDX + trivy

```bash
dotnet tool install --global CycloneDX

# 版本號從 csproj 的 VersionPrefix/Suffix 取得
V="$PREFIX-$SUFFIX"
dotnet-CycloneDX MyWebApp.sln -o .sbom -fn "MyWebApp.$V.cdx.json" --json

# 弱點：人看一份、機器讀一份
trivy sbom $SBOM --scanners vuln --format table
trivy sbom $SBOM --scanners vuln --format json

# 授權：先濾掉 Microsoft 發行的套件
trivy sbom $LIC_SBOM --scanners license --severity UNKNOWN,MEDIUM,HIGH,CRITICAL
```

1. **檔名帶版本**：SBOM 可對回發佈版本
2. **記得指定 JSON**：預設輸出 XML（bom.xml）；`-t` 可排除測試專案
3. **授權報告降噪**：python 濾掉 `System.`／`Microsoft.`／`runtime.`／`NETStandard.` 開頭元件
4. <span class="hl">**注意**</span>：前綴過濾可能誤排除同前綴的第三方套件

<!--
實測版本 6.2.0。腳本尚無實跑輸出紀錄，產出品質未驗證。
-->

---

<!-- _class: small -->

# 前端 JS：retire.js 補上 libman 函式庫

**為什麼不用 cyclonedx-npm？** 前端函式庫由 libman 放進 `wwwroot/lib`，沒有 package.json。retire.js 用檔案內容特徵辨識函式庫與版本。

```bash
retire --path MyWebApp/wwwroot/lib \
  --outputformat cyclonedxJSON --outputpath $JS_SBOM || true

cyclonedx-win-x64 merge --input-files $SBOM $JS_SBOM \
  --output-file $ALL_SBOM --output-format json
```

| 覆蓋缺口 | 說明 |
|---|---|
| CSS 不掃 | animate.css 不會出現在 SBOM |
| 部分函式庫辨識不到 | print-js、viewerjs 可能漏掉，需人工補登 |
| exit code 13 | 發現弱點時回傳 13，`set -e` 下會中斷 → 加 `\|\| true` 或 `--exitwith 0` |

---

<!-- _class: small -->

# 腳本全貌：一個指令，四份產出

```text
MyWebApp.sln ──→ dotnet-CycloneDX ──┐
                                    ├──→ cyclonedx-cli merge ──→ trivy sbom（vuln ×2、license ×1）
wwwroot/lib  ──→ retire.js ─────────┘

.sbom/
  {專案}.{版本}.cdx.json   合併後的 SBOM
  {專案}.{版本}.vuln.txt   弱點（人看）
  {專案}.{版本}.vuln.json  弱點（機器讀）
  {專案}.{版本}.lic.txt    授權風險
```

- **執行**：在方案根目錄 `bash dotnet-js-sbom-scan.sh`（Windows 用 Git Bash）
- **需要**：.NET SDK、dotnet-CycloneDX、trivy（需下載弱點 DB）、python 3、retire、cyclonedx-cli
- **收尾**：刪除中間檔，只留合併 SBOM 與三份報告

<!--
目前腳本裡專案名稱和路徑是寫死的，下一步是參數化後放進 CI。腳本尚無實跑輸出紀錄。
-->

---

# 兩條路線怎麼選

| | 路線一：syft + grype | 路線二：dotnet-CycloneDX + trivy |
|---|---|---|
| 輸入 | 發佈產物（dotnet publish） | 方案／專案檔（dotnet restore） |
| SBOM 類型（推論） | Analyzed | Source／Build |
| .NET 授權資訊 | 取不到 | 有，trivy license 掃描 |
| 前端 JS | 未涵蓋 | retire.js + cyclonedx-cli merge |
| 弱點比對 | grype | trivy |
| 適合 | 別人交付的產物、多生態系、容器 | 自家 .NET 專案、需要授權合規 |

> **我的選擇**：自家 .NET 專案走路線二，收到外部產物時用路線一交叉檢查。
> *兩條路線的元件清單是否一致，尚未實測比對。*

---

# 導入檢核清單

| 產生 | 掃描與保存 |
|---|---|
| ☑ 只掃要出貨的東西：publish 產物，或用 `-ef`／`-t` 排除 | ☑ 記錄工具版本與弱點 DB 建置時間 |
| ☑ 設定名稱與版本；檔名能對回製品 | ☑ 弱點報告留 table（人看）與 JSON（機器讀） |
| ☑ 清點沒有 purl 的元件 | ☑ 高風險弱點逐一研判，結論寫成 VEX |
| ☑ 確認元件有 license 欄位 | ☑ 保存 SBOM 與報告，排程重掃舊版本 |
| ☑ 檢查 retire 辨識結果，補登漏掉的函式庫 | ☑ 腳本參數化，放進 CI |

---

<!-- _class: dark -->

# 帶走三件事

1. **SBOM 是清單，不是保證**　要搭配弱點比對、VEX 研判與簽章才有用
2. **掃對範圍比掃得多重要**　1365 vs 176；沒有 purl、沒有 license 的元件就是盲點
3. **從一支腳本開始**　每次 build 產出 SBOM + 弱點 + 授權報告，再談 CI gate 與 VEX

## 下一步

Dependency-Track 集中管理 ・ Sigstore／in-toto 簽章 ・ 歐盟 CRA、CISA 2026 要素

---

<!-- _class: lead -->
<!-- _paginate: false -->
<!-- _footer: "" -->

# Q & A

回到開場的問題：下次 Log4Shell 發生時，你的團隊需要多久回答？
