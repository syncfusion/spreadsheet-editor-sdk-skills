# Merge Cells

> Merge two or more adjacent cells into a single cell in WPF Spreadsheet control.

---

## Overview

Allows combining multiple cells into one, displaying the content of a single cell across the merged area.

---

## Key Features
- Merge horizontally or vertically
- Unmerge cells
- Retain content of the top-left cell

---

## Example

Select a range and use the Merge command to combine cells. Unmerge to revert to individual cells.

## Merge Cells
```csharp
// To merge two or more cells in the spreadsheet
//spreadsheet.ActiveGrid.SelectionController.AddSelection(GridRangeInfo.Cells(4, 6, 5, 8));
var gridRange = spreadsheet.ActiveGrid.SelectedRanges.ActiveRange;
var excelRange = gridRange.ConvertGridRangeToExcelRange(spreadsheet.ActiveGrid);
var coverCell = new CoveredCellInfo(gridRange.Top, gridRange.Left, gridRange.Bottom, gridRange.Right);
spreadsheet.ActiveGrid.CoveredCells.Add(coverCell);
spreadsheet.ActiveSheet.Range[excelRange].Merge();
spreadsheet.ActiveGrid.InvalidateCell(gridRange, true);
```

## UnMerge Cells
```csharp
// To the merged cells in Spreadsheet
var gridRange = spreadsheet.ActiveGrid.SelectedRanges.ActiveRange;
var excelRange = gridRange.ConvertGridRangeToExcelRange(spreadsheet.ActiveGrid);
spreadsheet.ActiveGrid.CoveredCells.Clear(gridRange);
spreadsheet.ActiveSheet.Range[excelRange].UnMerge();
spreadsheet.ActiveGrid.InvalidateCell(gridRange, true);
```

---

## References
- [Merge Cells Documentation](https://help.syncfusion.com/wpf/spreadsheet/merge-cells)
