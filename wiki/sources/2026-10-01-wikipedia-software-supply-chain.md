---
title: Wikipedia：Software supply chain（英文）
type: source
tags: [sbom, supply-chain, wikipedia]
sources: [raw/industry/Software supply chain.md]
source_url: https://en.wikipedia.org/wiki/Software_supply_chain
source_author: Wikipedia 編者
source_date: 2015-01-16（頁面建立；剪藏內容含 2025–2026 年引用）
created: 2026-10-01
updated: 2026-10-01
status: draft
---

# Wikipedia：Software supply chain（英文）

## 基本資訊
- 類型：百科（二手彙整）
- 作者/發布者：Wikipedia 社群
- 發布日期：2015-01-16 建立；剪藏時間 2026-10-01
- 可信度評估：二手彙整；數據應回溯其引用的原始研究再採用

## 重點摘要
1. 軟體供應鏈 = 開發、建置、發布軟體製品所用的元件、函式庫、工具與流程；SBOM 是其元件清冊，為提升透明度的策略。
2. 背景數據：Synopsys 2024 分析，96% 商用程式碼庫含開源軟體；Linux Foundation 2022 報告，典型程式碼庫 70–90% 為開源元件。
3. 攻擊案例：SolarWinds（2020，超過 18,000 組織安裝惡意更新）、NotPetya（2017）、Kaseya（2021）、XZ Utils 後門（2024）；Heartbleed、Shellshock（2014）、Log4Shell（2021）凸顯 SCA 需求。
4. 三個互補安全屬性：validity（驗證）、separation（隔離）、transparency（透明）；SBOM 與 provenance 提供可見性，但可見性本身不保證完整性。
5. 採用現況：僅約 0.56% 熱門 GitHub 儲存庫含符合政策的 SBOM；不到半數專案於發布中附 SBOM 且多不完整；Java 生態系六種產生工具常過度回報元件；2023 企業調查約 60–76% 要求或整合 SBOM；2025 金融業調查 43% 正在產出 SBOM。
6. SBOM 不宜用試算表管理，應集中儲存於可被自動化系統查詢的儲存庫。
7. 法規脈絡：2014 年 Cyber Supply Chain Management and Transparency Act 未通過；EO 14028（2021-05-12）要求 NIST 與 NTIA 訂定指引；NTIA 最低要素分三類。

## 關鍵主張與數據
- 「only about 0.56% of popular GitHub repositories contain SBOMs created in accordance with formal security or compliance policies」— 意涵：實務採用遠落後於政策倡議。
- 「visibility alone cannot guarantee integrity」— 意涵：SBOM 需搭配簽章與 provenance。

## 影響的 wiki 頁面
- [[concepts/software-supply-chain]] — 新建
- [[concepts/sbom]] — 補充定義、用途、採用現況
- [[regulations/eo-14028]]、[[regulations/ntia-minimum-elements]] — 新建
- [[overview]] — 更新目前論點

## 與既有知識的關係
- 支持：[[sources/2026-10-01-wikipedia-zh-software-supply-chain]]（中文版為其較早、較短的對應版本）
- 矛盾：中文版稱 SBOM 格式有三種（含 SWID），本文未討論格式；見 [[concepts/sbom]] 的待驗證標註
- 新增：採用率與工具準確度的實證研究（2023–2025）

## 待追問題
- 上述研究原文（arXiv 2509.01255、JSS 2025 112540）值得放入 `raw/papers/`。
- Linux Foundation 2022 報告與 FINOS 2025 報告值得取得原文。
