
### 為何要使用此工具
因為 syft 本身對 NET Core 的支援相對不完整，經測試 syft 工具拿不到 NET 套件的授權資訊，這樣就無法快速檢查 license 是否核可。此工具對 NET 套件支援較完整。

### 安裝  CycloneDX module for.NET

```
> dotnet tool install --global CycloneDX

您可以使用下列命令來叫用工具: dotnet-CycloneDX
已成功安裝工具 'cyclonedx' ('6.2.0' 版)。
```

### 最簡單使用

```
> dotnet-CycloneDx QadbGraphQL.slnx -o .sbom

...略...
Creating CycloneDX BOM
Writing to: D:\AsvtGIT\QadbGraphQL\.sbom\bom.xml
```
產生 XML 格式的 cdx 檔。存入 `.sbom` 目錄。輸出預設檔名 `bom.xml`。

### 一般應用
```
> dotnet-CycloneDx QadbGraphQL.slnx -o .sbom -F Json -t -fn myproject-version-cdx.json

...略...
Creating CycloneDX BOM
Writing to: D:\AsvtGIT\QadbGraphQL\.sbom\myproject-version-cdx.json
```

產生 JSON 格式的 cdx 檔。存入 `.sbom` 目錄。並指定輸出檔名。

參數說明:
`-o .sbom` 輸出目錄 `.sbom`。
`-F Json`  指定格式為 Json，預設是 XML。
`-t` 排除測試專案。
`-fn myproject-version-cdx.json` 指定輸出檔名。
