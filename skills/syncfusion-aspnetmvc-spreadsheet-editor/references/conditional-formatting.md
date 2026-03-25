# Conditional Formatting

Apply rules to automatically format cells based on their values (e.g., highlight negatives in red, top 10% in green, data bars, color scales, icon sets).

## Minimal Code

```cshtml
@using Syncfusion.EJ2
@using Syncfusion.EJ2.Spreadsheet

@{
    // Data source
    var salesData = new List<object>()
    {
        new { Month = "Jan", Sales = 35 },
        new { Month = "Feb", Sales = 40 },
        new { Month = "Mar", Sales = 50 }
    };
}

@Html.EJS().Spreadsheet("spreadsheet").AllowConditionalFormat(true).Created("onCreated").Sheets(sheet =>
    {
        sheet.Name("Sales").Ranges(ranges =>
            {
                ranges.DataSource(salesData).StartCell("A1").Add();
            }).Add();
    }).Render()

<script>
    function onCreated() {
        var spreadsheet = document.getElementById("spreadsheet").ej2_instances[0];

        // === Type 1: GreaterThan / LessThan ===
        spreadsheet.conditionalFormat({
            type: 'GreaterThan',
            value: '1000',
            cFColor: 'GreenFT',
            range: 'B2:B100'
        });

        spreadsheet.conditionalFormat({
            type: 'LessThan',
            value: '500',
            cFColor: 'RedFT',
            range: 'B2:B100'
        });

        // === Type 2: Between ===
        spreadsheet.conditionalFormat({
            type: 'Between',
            value: '100,500',
            cFColor: 'BlueFT',
            range: 'D2:D100'
        });

        // === Type 3: AboveAverage ===
        spreadsheet.conditionalFormat({
            type: 'AboveAverage',
            cFColor: 'GreenFT',
            range: 'F2:F100'
        });

        // === Type 4: Top 10 Items ===
        spreadsheet.conditionalFormat({
            type: 'Top10Items',
            value: '10',
            cFColor: 'GreenFT',
            range: 'G2:G100'
        });

        // === Type 5: Color Scale ===
        spreadsheet.conditionalFormat({
            type: 'RYGColorScale',
            range: 'H2:H100'
        });

        // === Type 6: Icon Sets ===
        spreadsheet.conditionalFormat({
            type: 'ThreeTrafficLights1',
            range: 'I2:I100'
        });

        // === Type 7: Data Bars ===
        spreadsheet.conditionalFormat({
            type: 'BlueDataBar',
            range: 'J2:J100'
        });

        // === Clear Conditional Formatting Rules ===
        spreadsheet.clearConditionalFormat('E2:E30'); // Clear specific range
        spreadsheet.clearConditionalFormat();         // Clear all rules
    }
</script>

```

## Placeholders for Conditional Format
 
| Placeholder  | Description                                  | Example                                                             |
|--------------|----------------------------------------------|---------------------------------------------------------------------|
| `[TYPE]`     | Specifies the conditional formatting type    | `'HighlightCell'`, `'TopBottom'`, `'DataBar'`, `'ColorScale'`, `'IconSet'` |
| `[VALUE]`    | Specifies the conditional formatting value   | `'string'`                                                          |
| `[CFCOLOR]`  | Specifies the highlight color style          | `'RedFT'`, `'GreenFT'`, `'YellowFT'`                               |
| `[FORMAT]`   | Specifies the format model                   | `'FormatModel'`                                                     |
| `[RANGE]`    | Specifies the conditional formatting range   | `'A1:A10'`, `'Sheet1!A1:A10'`                                       |


## Type Definitions
 
### HighlightCell
```cshtml
type HighlightCell = 'GreaterThan' | 'LessThan' | 'Between' | 'EqualTo' |
  'ContainsText' | 'DateOccur' | 'Duplicate' | 'Unique';
```
 
### TopBottom
```cshtml
type TopBottom = 'Top10Items' | 'Bottom10Items' | 'Top10Percentage' |
  'Bottom10Percentage' | 'BelowAverage' | 'AboveAverage';
```
 
### DataBar
```cshtml
type DataBar = 'BlueDataBar' | 'GreenDataBar' | 'RedDataBar' |
  'OrangeDataBar' | 'LightBlueDataBar' | 'PurpleDataBar';
```
 
### ColorScale
```cshtml
type ColorScale = 'GYRColorScale' | 'RYGColorScale' | 'GWRColorScale' |
  'RWGColorScale' | 'BWRColorScale' | 'RWBColorScale' | 'WRColorScale' |
  'RWColorScale' | 'GWColorScale' | 'WGColorScale' | 'GYColorScale' | 'YGColorScale';
```
 
### IconSet
```cshtml
type IconSet = 'ThreeArrows' | 'ThreeArrowsGray' | 'FourArrowsGray' |
  'FourArrows' | 'FiveArrowsGray' | 'FiveArrows' | 'ThreeTrafficLights1' |
  'ThreeTrafficLights2' | 'ThreeSigns' | 'FourTrafficLights' | 'FourRedToBlack' |
  'ThreeSymbols' | 'ThreeSymbols2' | 'ThreeFlags' | 'FourRating' | 'FiveQuarters' |
  'FiveRating' | 'ThreeTriangles' | 'ThreeStars' | 'FiveBoxes';
```

## Color Format Values (`cFColor`)
 
The `cFColor` property specifies the fill and text color using built-in Syncfusion styles.
 
| Value         | Description              |
|---------------|--------------------------|
| `'RedFT'`     | Red fill, text           |
| `'YellowFT'`  | Yellow fill, text        |
| `'GreenFT'`   | Green fill, text         |
| `'RedF'`      | Red fill only            |
| `'RedT'`      | Red text only            |
 
## FormatModel
 
Interface for a class Format used in conditional formatting.
 
| Property    | Description                        | Example        |
|-------------|------------------------------------|----------------|
| `format`    | Specifies the number format        | `'$#,##0.00'`  |
| `isLocked`  | Specifies if the cell is locked    | `true`/`false` |
| `style`     | Specifies the cell style           | `StyleModel`   |
