# 調整現有規則 SOP

以 SA1201 為例，調整一個現有規則需依序處理以下檔案。

## 1. 核心實作（必改）

**`StyleCop.Analyzers/OrderingRules/SA1201ElementsMustAppearInTheCorrectOrder.cs`**

- 規則的分析邏輯
- `HelpLink` 常數——若有自己的文件站需更新連結：
  ```csharp
  private const string HelpLink = "https://github.com/.../documentation/SA1201.md";
  ```

## 2. 資源文字（視情況）

**`StyleCop.Analyzers/OrderingRules/OrderingResources.resx`**

- 規則的 Title、MessageFormat、Description
- 注意：`Lightup/.generated/` 下的 `.Designer.cs` 是自動產生，不要直接修改

## 3. 文件（視情況）

**`documentation/SA1201.md`**

- 說明規則原因（Cause）、規則說明（Rule description）、修正方式（How to fix violations）、suppress 範例
- 需與程式碼行為保持一致，手動維護

## 4. Code Fix（如有）

**`StyleCop.Analyzers.CodeFixes/OrderingRules/ElementOrderCodeFixProvider.cs`**

## 5. 測試（應一起更新）

- `StyleCop.Analyzers.Test/OrderingRules/SA1201UnitTests.cs`（主要）
- `StyleCop.Analyzers.Test.CSharp{7~13}/OrderingRules/SA1201CSharp*UnitTests.cs`（各版本）

## 6. 執行單元測試

修改完成後，執行所有相關版本的測試確認無誤：

```powershell
# 跑全解決方案中所有 SA1201 相關測試（含 CSharp7~13）
dotnet test ./StyleCopAnalyzers.sln --filter "FullyQualifiedName~SA1201"
```
也可使用Visual Studio內的Test Explorer測試功能

測試說明：
- `SA1201UnitTests.cs`（無版本後綴）預設使用 **C# 10**
- `SA1201CSharp{7~13}UnitTests.cs` 各自對應特定 C# 版本的語法測試

## 7. 版本紀錄（視情況）

**`StyleCop.Analyzers/AnalyzerReleases.Shipped.md`**

- 僅在行為有 breaking change 時需要記錄

## 7. 版本號（視情況）

**`version.json`**（專案根目錄）

- 修改 `version` 欄位後需 commit 才會生效
- Build 時由 Nerdbank.GitVersioning 自動寫入 dll
