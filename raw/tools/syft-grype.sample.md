# syft + grype 使用範例：產生 SBOM 並掃描漏洞

以 AsvtQUO 專案為例，用 [syft](https://github.com/anchore/syft) 產生 CycloneDX 格式的 SBOM，再用 [grype](https://github.com/anchore/grype) 掃描已知漏洞。

> 環境：Windows 11 + Git Bash，syft 1.52.0、grype 0.119.0。

## 1. 安裝與確認版本

兩者皆可透過 winget 安裝，安裝後需重開終端機讓 PATH 生效。

```bash
winget install Anchore.Syft
winget install Anchore.Grype

syft --version     # syft 1.52.0
grype --version    # grype 0.119.0
```

## 2. 用 syft 產生 SBOM

### 2.1 掃描整個專案目錄

```bash
syft dir:. -o cyclonedx-json=sbom.cdx.json
```

- `dir:.`：掃描目前目錄。
- `-o cyclonedx-json=<檔名>`：輸出 CycloneDX JSON 並寫入檔案。

整個目錄會連 `bin/`、`obj/`、`publish/` 等建置產物一起掃描，套件重複計算（本例 1365 個元件）。可用 `--exclude` 排除：

```bash
syft dir:. --exclude './**/bin/**' --exclude './publish/**' -o cyclonedx-json=sbom.cdx.json
```

### 2.2 只掃描發佈產物（建議）

```bash
syft dir:publish -o cyclonedx-json=publish.sbom.cdx.json
```

只含實際部署的內容（本例 176 個元件），較貼近正式環境。

### 2.3 指定名稱與版本

未指定時 syft 會警告：

```
WARN no explicit name and version provided for directory source, deriving artifact ID from the given path (which is not ideal)
```

正式交付時建議加上 `--source-name` 與 `--source-version`。版本可對照 `publish/AsvtQUO.deps.json` 中的 `"AsvtQUO/1.7.14-release"`：

```bash
syft dir:publish --source-name AsvtQUO --source-version 1.7.14-release -o cyclonedx-json=publish.sbom.cdx.json
```

產出 SBOM 的 `metadata.component` 即為 `AsvtQUO` / `1.7.14-release`。

## 3. 用 grype 掃描漏洞

### 3.1 漏洞資料庫

首次執行會自動下載漏洞資料庫。

```bash
grype db status    # 查看資料庫版本、建置時間與狀態
grype db update    # 手動更新資料庫
```

`grype db status` 輸出範例：

```
Path:      %LOCALAPPDATA%\cache\grype\db\6\vulnerability.db
Schema:    v6.1.9
Built:     2026-09-30T06:32:47Z
Status:    valid
```

### 3.2 掃描 SBOM（表格輸出）

```bash
grype sbom:publish.sbom.cdx.json -o table
```

無漏洞時輸出：

```
No vulnerabilities found
```

### 3.3 掃描 SBOM（JSON 輸出）

```bash
grype sbom:sbom.cdx.json -o json > sbom.grype.json
```

JSON 中的 `matches` 為比對到的漏洞，`ignoredMatches` 為被忽略的項目；兩者皆為空陣列即代表無已知漏洞。

## 4. 掃描結果（2026-10-01）

| SBOM | 元件數 | 漏洞數 |
|------|-------:|-------:|
| `sbom.cdx.json`（整個專案目錄） | 1365 | 0 |
| `publish.sbom.cdx.json`（發佈產物） | 176 | 0 |

注意：grype 只能比對有 purl 的套件（本例為 NuGet 套件）；無 purl 的元件與 .NET 執行環境本身不在掃描範圍內。
