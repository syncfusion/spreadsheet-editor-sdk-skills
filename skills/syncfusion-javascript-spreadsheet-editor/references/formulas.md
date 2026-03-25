# Formulas & Calculations

Use the built-in formula engine to perform calculations, aggregates, and named ranges in the Syncfusion EJ2 Spreadsheet.

## Table of Contents

- [Minimal Code](#minimal-code)
  - [Option 1: Enter a formula in a single cell](#option-1-enter-a-formula-in-a-single-cell)
  - [Option 2: Enter formula in multiple cells](#option-2-enter-formula-in-multiple-cells)
  - [Option 3: Named ranges](#option-3-named-ranges)
  - [Option 4: Formula via CellModel](#option-4-formula-via-cellmodel-inline-sheet-definition)
  - [Option 5: Cross-sheet reference](#option-5-cross-sheet-reference)
  - [Option 6: Show aggregate in status bar](#option-6-show-aggregate-in-status-bar)
- [Placeholders](#placeholders)
  - [enableFormula](#enableformula-spreadsheet-property)
  - [updateCell](#updatecellcell-address)
  - [addDefinedName](#adddefinednamedefinedname)
  - [removeDefinedName](#removedefinednamedefinedname-scope)
  - [CellModel](#cellmodel-inline-rowscells)
- [Supported Formula Categories](#supported-formula-categories)
  - [Math & Trigonometry](#math--trigonometry)
  - [Statistical](#statistical)
  - [Logical](#logical)
  - [Lookup & Reference](#lookup--reference)
  - [Text](#text)
  - [Date & Time](#date--time)
- [Cell Reference Types](#cell-reference-types)
- [Notes](#notes)

---

## Minimal Code

```typescript
import { Spreadsheet } from '@syncfusion/ej2-spreadsheet';

const spreadsheet = new Spreadsheet({
  enableFormula: true,           // Enable formula support
  sheets: [{ name: 'Sheet1' }]
});

spreadsheet.appendTo('#spreadsheet');

// === Option 1: Enter a formula in a single cell ===
spreadsheet.updateCell(
  { value: '=SUM(B2:B10)' },
  'B11'
);

// === Option 2: Enter formula in multiple cells ===
const salesData = [
  { Product: 'Laptop', Price: 1200, Quantity: 5 },
  { Product: 'Mouse', Price: 25, Quantity: 20 },
  { Product: 'Keyboard', Price: 80, Quantity: 10 }
];

spreadsheet.sheets[0].ranges = [{ dataSource: salesData, startCell: 'A1' }];

// Add formula to Total column (D2:D4)
for (let i = 0; i < salesData.length; i++) {
  const row = i + 2;
  spreadsheet.updateCell({ value: `=B${row}*C${row}` }, `D${row}`);
}

// Aggregate at the bottom
spreadsheet.updateCell({ value: '=SUM(D2:D4)' }, 'D5');
spreadsheet.updateCell({ value: '=AVERAGE(D2:D4)' }, 'D6');
spreadsheet.updateCell({ value: '=COUNT(D2:D4)' }, 'D7');
spreadsheet.updateCell({ value: '=MAX(D2:D4)' }, 'D8');
spreadsheet.updateCell({ value: '=MIN(D2:D4)' }, 'D9');

// === Option 3: Named ranges ===
spreadsheet.addDefinedName({
  name: 'PriceRange',
  refersTo: '=Sheet1!B2:B4',
  scope: 'Workbook',
  comment: 'Product prices'
});

spreadsheet.updateCell({ value: '=SUM(PriceRange)' }, 'F2');

// Remove a named range
spreadsheet.removeDefinedName('PriceRange', 'Workbook');

// === Option 4: Formula via CellModel (inline sheet definition) ===
// Use `formula` property (not `value`) when defining cells inside rows[]
const spreadsheetInline = new Spreadsheet({
  enableFormula: true,
  sheets: [{
    name: 'Sheet1',
    rows: [
      {
        cells: [
          { value: 'Product' }, { value: 'Price' }, { value: 'Qty' }, { value: 'Total' }
        ]
      },
      {
        cells: [
          { value: 'Laptop' }, { value: '1200' }, { value: '5' },
          { formula: '=B2*C2' }
        ]
      },
      {
        cells: [
          { value: 'Mouse' }, { value: '25' }, { value: '20' },
          { formula: '=B3*C3' }
        ]
      },
      {
        cells: [
          { value: 'Totals', style: { fontStyle: 'italic', fontWeight: 'bold' } },
          { formula: '=SUM(B2:B3)' },
          { formula: '=SUM(C2:C3)' },
          { formula: '=SUM(D2:D3)' }
        ]
      }
    ]
  }]
});

spreadsheetInline.appendTo('#spreadsheet');

// === Option 5: Cross-sheet reference ===
spreadsheet.updateCell(
  { value: '=Sheet1!B2+Sheet1!C2' },
  'A1'
);

// === Option 6: Show aggregate in status bar ===
const spreadsheetWithAgg = new Spreadsheet({
  enableFormula: true,
  showAggregate: true,
  sheets: [{ name: 'Sheet1' }]
});
```

## Placeholders

### `enableFormula` (Spreadsheet property)

| Placeholder | Description | Example |
|---|---|---|
| `enableFormula` | Enables formula parsing and calculation engine | `true`, `false` |

### `updateCell(cell, address)`

| Placeholder | Description | Example |
|---|---|---|
| `value` | Formula string — must start with `=` | `'=SUM(A1:A10)'`, `'=IF(A1>0,"Yes","No")'`, `'=B2*C2'` |
| `address` | Target cell address | `'B11'`, `'D5'`, `'A1'` |

### `addDefinedName(definedName)`

| Placeholder | Description | Example |
|---|---|---|
| `name` | Unique name for the named range | `'PriceRange'`, `'TotalRevenue'` |
| `refersTo` | Cell/range reference — must start with `=` | `'=Sheet1!B2:B4'`, `'=Sheet1!A1:D10'` |
| `scope` | Scope of the named range | `'Workbook'`, `'Sheet1'` |
| `comment` | Optional description for the name | `'Monthly sales data'` |

### `removeDefinedName(definedName, scope)`

| Placeholder | Description | Example |
|---|---|---|
| `definedName` | Name to remove | `'PriceRange'` |
| `scope` | Scope where name was defined | `'Workbook'`, `'Sheet1'` |

### CellModel (inline `rows[].cells[]`)

| Placeholder | Description | Example |
|---|---|---|
| `formula` | Formula string on `CellModel` — used in `rows[].cells[]` inline definition | `'=SUM(B2:B10)'`, `'=B2*C2'` |
| `value` | Plain text or number value | `'Laptop'`, `'1200'` |

## Supported Formula Categories

### Math & Trigonometry
```typescript
'=SUM(A1:A10)'           // Sum of a range
'=SUMIF(A1:A10,">5")'    // Conditional sum
'=ROUND(A1,2)'           // Round to 2 decimal places
'=ABS(A1)'               // Absolute value
'=MOD(A1,3)'             // Remainder
'=POWER(A1,2)'           // A1 squared
'=SQRT(A1)'              // Square root
```

### Statistical
```typescript
'=AVERAGE(A1:A10)'        // Average of range
'=AVERAGEIF(A1:A10,">5")' // Conditional average
'=COUNT(A1:A10)'          // Count numeric cells
'=COUNTA(A1:A10)'         // Count non-empty cells
'=MAX(A1:A10)'            // Maximum value
'=MIN(A1:A10)'            // Minimum value
'=MEDIAN(A1:A10)'         // Median value
```

### Logical
```typescript
'=IF(A1>0,"Positive","Negative")'  // Conditional
'=AND(A1>0,B1>0)'                  // Logical AND
'=OR(A1>0,B1>0)'                   // Logical OR
'=NOT(A1>0)'                       // Logical NOT
'=IFERROR(A1/B1,0)'                // Error handling
```

### Lookup & Reference
```typescript
'=VLOOKUP(A1,B1:D10,2,FALSE)'      // Vertical lookup
'=HLOOKUP(A1,B1:D10,2,FALSE)'      // Horizontal lookup
'=INDEX(A1:D10,2,3)'               // Index lookup
'=MATCH(A1,B1:B10,0)'              // Match position
'=OFFSET(A1,1,0,3,1)'             // Offset reference
```

### Text
```typescript
'=CONCATENATE(A1," ",B1)'          // Join text
'=LEFT(A1,3)'                      // Left characters
'=RIGHT(A1,3)'                     // Right characters
'=MID(A1,2,4)'                     // Middle characters
'=LEN(A1)'                         // String length
'=UPPER(A1)'                       // Uppercase
'=LOWER(A1)'                       // Lowercase
'=TRIM(A1)'                        // Remove extra spaces
```

### Date & Time
```typescript
'=TODAY()'                         // Current date
'=NOW()'                           // Current date and time
'=DATE(2025,1,1)'                  // Specific date
'=YEAR(A1)'                        // Extract year
'=MONTH(A1)'                       // Extract month
'=DAY(A1)'                         // Extract day
'=DATEDIF(A1,B1,"D")'             // Days between dates
```

## Cell Reference Types

```typescript
// Relative reference — shifts when copied
'=A1+B1'

// Absolute reference — stays fixed when copied
'=$A$1+$B$1'

// Mixed reference — one part fixed
'=$A1'    // Column fixed, row shifts
'=A$1'    // Row fixed, column shifts

// Cross-sheet reference
'=Sheet2!A1'
'=Sheet2!A1:B10'
```

## Notes

- **Required**: Set `enableFormula: true` on the Spreadsheet instance for formula support
- **Functions Supported**: All standard Excel functions (SUM, AVERAGE, VLOOKUP, IF, etc.)
- **`formula` vs `value`**: Use `formula` property in `rows[].cells[]`; use `value: '=...'` when calling `updateCell()` programmatically
- **Gotcha**: Using `value: '=SUM(...)'` inside `rows[].cells[]` may not evaluate — use `formula` instead
- **Named Ranges**: `refersTo` must include `=` prefix (e.g., `'=Sheet1!B2:B4'`)
- **Named Ranges**: Must be defined before use in formulas
- **`addDefinedName`**: Returns `boolean` — check for `false` to detect duplicate name conflicts
- **`showAggregate`**: Displays sum/avg/count in the status bar when a range is selected
- **Cross-sheet**: Use `SheetName!CellAddress` syntax for cross-sheet references
- **Best Practice**: Use named ranges for frequently referenced ranges to improve readability
- **Best Practice**: Use `IFERROR` to gracefully handle division-by-zero and missing values
- **Gotcha**: Formulas referencing empty cells return `0` — use `IF` or `IFERROR` to handle this