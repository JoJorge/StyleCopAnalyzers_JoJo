# Alternative Rules (SX0000-)

非標準的 StyleCop 擴充規則，代表部分專案採用的替代風格。這些規則與標準 StyleCop 規則直接衝突，啟用時需停用對應的標準規則。

---

## SX1101 — DoNotPrefixLocalMembersWithThis

呼叫本地類別或基底類別的實例成員時加了 `this.` 前綴。此規則與 SA1101 直接衝突，**啟用此規則時應停用 SA1101**。

例外：當方法參數名稱與 `this.` 後的識別符衝突時不觸發。

**範例：**
```csharp
// 正確（SX1101 啟用時）
Initialize();
Name = "Test";

// 錯誤（SX1101 啟用時）
this.Initialize();
this.Name = "Test";
```

---

## SX1309 — FieldNamesMustBeginWithUnderscore

private instance 欄位名稱未以底線開頭。

只檢查 private instance 欄位，忽略：`static`、`const`、public/internal 欄位、static `readonly` 欄位（視為常數）。C# 8 readonly struct 成員（方法、屬性等）不受此規則影響。模式比對的捨棄指示符（`_`）不是欄位，不受影響。

**範例：**
```csharp
// 正確
private int _count;
private readonly string _name;

// 錯誤
private int count;
private readonly string name;
```

---

## SX1309S — StaticFieldNamesMustBeginWithUnderscore

private static 欄位名稱未以底線開頭。

只檢查 private static 欄位，且排除 `const` 與 `readonly`（static readonly 視為常數）。

**範例：**
```csharp
// 正確
private static int _instanceCount;

// 錯誤
private static int instanceCount;
```

---

*來源：[`documentation/AlternativeRules.md`](../documentation/AlternativeRules.md) 及對應各規則 `.md` 檔。*
