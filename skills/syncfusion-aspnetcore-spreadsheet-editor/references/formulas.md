# Formulas & Calculations

Use the built-in formula engine to perform calculations, aggregates, and references in cells.

## Minimal Code

```cshtml
@using Syncfusion.EJ2.Spreadsheet

<div class="control-pane">
    <div class="control-section spreadsheet-control">
        <ejs-spreadsheet id="spreadsheet" showAggregate="true" created="onCreated">
            <e-spreadsheet-sheets>
                <e-spreadsheet-sheet name="Sheet1">
                </e-spreadsheet-sheet>
            </e-spreadsheet-sheets>
        </ejs-spreadsheet>
    </div>
</div>

<script>
    //Bind created event to perform the action during initial load.
    function onCreated() {
        var spreadsheet = document.getElementById("spreadsheet").ej2_instances[0]; 

        // === Option 1: Enter formula in a cell programmatically ===
        spreadsheet.updateCell(
            { formula: '=SUM(B2:B10)' },    // Formula as string
            'B11'                          // Target cell address
        );

        // === Option 2: Enter formula in multiple cells (e.g., total column) ===
        var salesData = [
            { Product: 'Laptop', Price: 1200, Quantity: 5 },
            { Product: 'Mouse', Price: 25, Quantity: 20 },
            { Product: 'Keyboard', Price: 80, Quantity: 10 }
        ];

        // First bind data (see data-binding.md)
        spreadsheet.sheets[0].ranges = [{ dataSource: salesData, startCell: 'A2' }];

        // Add formula in Total column (D2:D4)
        for (var i = 0; i < salesData.length; i++) {
            var row = i + 2; // rows start from 2 (after header)
            spreadsheet.updateCell(
                { formula: '=B' + row + '*C' + row },
                'D' + row
            );
        }

        // Add SUM at bottom
        spreadsheet.updateCell(
            { formula: '=SUM(D2:D4)' },
            'D5'
        );

        // === Option 3: Add Named range example ===
        spreadsheet.addDefinedName({
            name: 'SalesRange',
            refersTo: '=Sheet1!B2:B4'   // Price column
        });

        spreadsheet.updateCell(
            { formula: '=SUM(SalesRange)' },
            'E2'                        // Total sales
        );

        // === Option 4: Aggregate display (status bar style) ===
        // showAggregate is a Spreadsheet property (set at initialization or via setProperties)
        // It shows sum/avg/count in the bottom status bar when cells are selected
    }
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

- Use named ranges for frequently referenced ranges
- Use semicolons (;) or commas (,) depending on locale (`listSeparator` property)
