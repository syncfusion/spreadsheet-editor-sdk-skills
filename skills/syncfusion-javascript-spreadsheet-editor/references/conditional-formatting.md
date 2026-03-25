# Conditional Formatting

Apply rules to automatically format cells based on their values (e.g., highlight negatives in red, top 10% in green, data bars, color scales, icon sets).

## Minimal Code

```typescript
import { Spreadsheet } from '@syncfusion/ej2-spreadsheet';

// Initialize spreadsheet with conditional formatting enabled
const spreadsheet: Spreadsheet = new Spreadsheet({
  allowConditionalFormat: true,
  sheets: [{ name: 'Sales' }]
});

spreadsheet.appendTo('#spreadsheet');

// Apply blue data bar to the specified range
spreadsheet.conditionalFormat({ type: 'BlueDataBar', range: 'D3:D18' });

// Apply three stars icon set to the specified range
spreadsheet.conditionalFormat({ type: 'ThreeStars', range: 'F3:F18' });

// Highlight cells with a value greater than the specified value
spreadsheet.conditionalFormat({ type: 'GreaterThan', cFColor: 'RedFT', value: '10/15/2023', range: 'E2:E30' });

// Highlight cells with a value between specified range
spreadsheet.conditionalFormat({ type: 'Between', cFColor: 'GreenFT', value: '03/04/2023,06/26/2023', range: 'E2:E30' });

// Highlight cells with a value above average of the specified range
spreadsheet.conditionalFormat({ type: 'AboveAverage', cFColor: 'RedFT', range: 'F2:F30' });

// Apply RYG (Red-Yellow-Green) color scale to the specified range
spreadsheet.conditionalFormat({ type: 'RYGColorScale', range: 'F2:F30' });

// Clear rules from a specific range
spreadsheet.clearConditionalFormat('E2:E30');

// Clear rules using sheet name in the range
spreadsheet.clearConditionalFormat('Sheet1!F2:F30');

// Clear all rules from the active sheet
spreadsheet.clearConditionalFormat();
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
```typescript
type HighlightCell = 'GreaterThan' | 'LessThan' | 'Between' | 'EqualTo' |
  'ContainsText' | 'DateOccur' | 'Duplicate' | 'Unique';
```

### TopBottom
```typescript
type TopBottom = 'Top10Items' | 'Bottom10Items' | 'Top10Percentage' |
  'Bottom10Percentage' | 'BelowAverage' | 'AboveAverage';
```

### DataBar
```typescript
type DataBar = 'BlueDataBar' | 'GreenDataBar' | 'RedDataBar' |
  'OrangeDataBar' | 'LightBlueDataBar' | 'PurpleDataBar';
```

### ColorScale
```typescript
type ColorScale = 'GYRColorScale' | 'RYGColorScale' | 'GWRColorScale' |
  'RWGColorScale' | 'BWRColorScale' | 'RWBColorScale' | 'WRColorScale' |
  'RWColorScale' | 'GWColorScale' | 'WGColorScale' | 'GYColorScale' | 'YGColorScale';
```

### IconSet
```typescript
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