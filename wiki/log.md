---
title: 知識庫紀錄
type: overview
tags: [log]
created: 2026-10-01
updated: 2026-10-01
---

# 知識庫紀錄（Log）

> 只能 append。查詢最近紀錄：`grep "^## \[" wiki/log.md | tail -5`

## [2026-10-01] setup | 建立 SBOM 研究 LLM Wiki 骨架
- 依 Karpathy LLM Wiki 模式建立三層架構：`raw/`、`wiki/`、`CLAUDE.md`
- 建立頁面範本：source、concept、standard、tool、regulation、organization、practice、analysis
- 新增：[[overview]]、[[index]]，以及 stub 頁 [[concepts/sbom]]、[[concepts/vex]]、[[standards/spdx]]、[[standards/cyclonedx]]
- 下一步：依 [[overview]] 的研究路線圖蒐集第一批來源放入 `raw/`
