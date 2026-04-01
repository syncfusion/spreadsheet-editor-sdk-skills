## Add a Worksheet

**Method:** `AddSheet()` on `Spreadsheet`

```csharp
spreadsheet.AddSheet();
```

To add a worksheet at a specific position:

```csharp
spreadsheet.AddSheet("Sheet4", 3);
```

## Remove a Worksheet

```csharp
spreadsheet.RemoveSheet("Sheet2");
```

## Rename a Worksheet

```csharp
//To Rename a sheet programmatically
spreadsheet.RenameSheet("ExistingSheetName", "NewSheetName");
```

## Navigate Between Worksheets

**Property:** `ActiveSheet` on `Spreadsheet`

```csharp
// Set the active sheet using the provided sheet name. If no sheet name is specified, use the default sheet names (e.g., Sheet1 for the first sheet, Sheet2 for the second sheet, and so on).
spreadsheet.SetActiveSheet("Sheet5");
```

## Access Worksheets

```csharp
// Access by index:
IWorksheet sheet = spreadsheet.Workbook.Worksheets[0];

// Access by name:
IWorksheet sheet = spreadsheet.Workbook.Worksheets["Sheet1"];

// Get total worksheet count:
int count = spreadsheet.Workbook.Worksheets.Count;
```

## Accessing the cell or range of cells

```csharp
// Access a cell by specifying cell address. 
var cell = spreadsheet.Workbook.Worksheets[0].Range["A3"];

// Access a cell by specifying cell row and column index. 
var cell1 = spreadsheet.Workbook.Worksheets[0].Range[3, 1];

// Access a cells by specifying user defined name.
var cell2 = spreadsheet.Workbook.Worksheets[0].Range["Namerange"];

// Accessing a range of cells by specifying cell's address.
var cell3 = spreadsheet.Workbook.Worksheets[0].Range["A5:C8"];

// Accessing a range of cells specifying cell row and column index.
var cell4 = spreadsheet.Workbook.Worksheets[0].Range[15, 1, 15, 3];
```

## Accessing the value of a cell
```csharp
// Access a cell value by using "Value" Property,
var cellValue = spreadsheet.Workbook.Worksheets[1].Range["A3"].Value

// Access a cell value by using "DisplayText" Property. 
var displayValue = spreadsheet.Workbook.Worksheets[1].Range[4, 1].DisplayText;
```

## Formula Bar

```csharp
spreadsheet.FormulaBarVisibility = true;
```

## Show or Hide a Worksheet

```csharp
//Hide Sheet
spreadsheet.HideSheet("Sheet2");

//Unhide Sheet
spreadsheet.UnhideSheet("Sheet2");
```

## Gridlines
```csharp
//To show GridLines
spreadsheet.SetGridLinesVisibility(true);

//To hide GridLines
spreadsheet.SetGridLinesVisibility(false);
```

## Headings
```csharp
//To hide the Header cells visibility
spreadsheet.SetRowColumnHeadersVisibility(false);
```

## Zooming
```csharp
//zoom factor
spreadsheet.SetZoomFactor("Sheet1", 200);
```
## Worksheet Events

| Event | Description |
|---|---|
| `WorkbookLoaded` | Occurs after a workbook is loaded into the Spreadsheet. |
| `SheetAdded` | Occurs when a new worksheet is added. |
| `SheetRemoved` | Occurs when a worksheet is removed. |
| `ActiveSheetChanged` | Occurs when the active worksheet is changed. |

## See Also

- [Getting Started](getting-started.md)
- [Editing](editing.md)
- [Protection](protection.md)
