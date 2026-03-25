# Formulas & Calculations

Use the built-in formula engine to perform calculations, aggregates, and references in cells.

## Minimal Code

```vue
<template>
<div class="control-section">
  <ejs-spreadsheet
    ref="spreadsheet"
    :showAggregate="true"
    :created="onCreated"
  >
    <e-sheets>
      <e-sheet name="Sheet1">
        <e-ranges>
          <e-range :dataSource="salesData" startCell="A2" />
        </e-ranges>
      </e-sheet>
    </e-sheets>
  </ejs-spreadsheet>
</div>
</template>

<script>
import {
SpreadsheetComponent,
SheetsDirective,
SheetDirective,
RangesDirective,
RangeDirective
} from "@syncfusion/ej2-vue-spreadsheet";

export default {
components: {
  "ejs-spreadsheet": SpreadsheetComponent,
  "e-sheets": SheetsDirective,
  "e-sheet": SheetDirective,
  "e-ranges": RangesDirective,
  "e-range": RangeDirective
},

data: () => ({
  salesData: [
    { Product: "Laptop", Price: 1200, Quantity: 5 },
    { Product: "Mouse", Price: 25, Quantity: 20 },
    { Product: "Keyboard", Price: 80, Quantity: 10 }
  ]
}),

methods: {
  onCreated() {
    const spreadsheet = this.$refs.spreadsheet;
    // === Formula in single cell ===
    spreadsheet.updateCell({ formula: "=SUM(B2:B10)" }, "B11");
    // === Bind data to sheet ===
    spreadsheet.ej2Instances.sheets[0].ranges = [{ dataSource: this.salesData, startCell: "A1" }];
    // === Add formulas for totals (D2:D4) ===
    this.salesData.forEach((_, i) => {
      const r = i + 2;
      spreadsheet.updateCell({ formula: `=B${r}*C${r}` }, `D${r}`);
    });
    // === SUM of totals row ===
    spreadsheet.updateCell({ formula: "=SUM(D2:D4)" }, "D5");
    // === Define named range ===
    spreadsheet.addDefinedName({
      name: "SalesRange",
      refersTo: "=Sheet1!B2:B4"
    });
    // === Use named range in a formula ===
    spreadsheet.updateCell({ formula: "=SUM(SalesRange)" }, "E2");
  }
}
};
</script>
```

## Placeholders

| Placeholder | Description | Example |
|---|---|---|
| `[FORMULA]` | Excel formula string | `'=SUM(A1:A10)'`, `'=AVERAGE(B1:B20)'` |
| `[RANGE]` | Cell range for formula | `'A1:D100'` |
| `[NAMED_RANGE]` | User-defined range name | `'SalesData'`, `'TotalRevenue'` |
| `[FUNCTION_NAME]` | Formula function name | `'SUM'`, `'AVERAGE'`, `'VLOOKUP'` |
| `[ARGUMENTS]` | Formula function arguments | `'A1:A10'`, `'A1:A10, 2, FALSE'` |

## Notes

- **Best Practice**: Use named ranges for frequently referenced ranges
- **Best Practice**: Prefix custom function names to avoid conflicts (see `custom-functions.md`)
- **Formula Syntax**: Use semicolons (;) or commas (,) depending on locale (`listSeparator` property)
- **Functions Supported**: All Excel functions (SUM, AVERAGE, VLOOKUP, IF, etc.)
- **Aggregates**: SUBTOTAL ignores hidden rows; `showAggregate` enables the status bar display
- **Named Ranges**: Use `addDefinedName()` method; `refersTo` must include `=` prefix (e.g., `'=Sheet1!B2:B4'`)
- **Remove Named Range**: Use `removeDefinedName(name, scope)` where scope is `'Workbook'` or sheet name
- **Performance**: Complex formulas on many cells can slow recalculation; use `calculationMode: 'Manual'` for large sheets
