# Custom Functions

Add custom calculation functions to extend the built-in formula engine in the Spreadsheet.

## Key Method

### `addCustomFunction(functionHandler, functionName?, formulaDescription?)`

| Parameter | Type | Required | Description |
|---|---|---|---|
| `functionHandler` | `string \| Function` | ✅ | Global handler name or function reference |
| `functionName` | `string` | ❌ | Formula name used in cells (uppercase) |
| `formulaDescription` | `string` | ❌ | Description shown in formula UI |

**Returns**: `void`

## Minimal Code

```typescript
import { Spreadsheet } from '@syncfusion/ej2-spreadsheet';

const spreadsheet = new Spreadsheet({
  sheets: [{ name: 'Sheet1' }],
  created: (): void => {
    // Register custom functions
    spreadsheet.addCustomFunction('DoubleHandler', 'DOUBLE', 'Multiplies value by 2');
    spreadsheet.addCustomFunction('FahrenheitHandler', 'FTOC', 'Fahrenheit to Celsius');
    spreadsheet.addCustomFunction('GradeHandler', 'GRADE', 'Returns letter grade');
  }
});

spreadsheet.appendTo('#spreadsheet');

// Define handlers in global (window) scope
(window as any).DoubleHandler = (num: number): number => num * 2;

(window as any).FahrenheitHandler = (f: number): number => (f - 32) * (5 / 9);

(window as any).GradeHandler = (score: number): string => {
  if (score >= 90) return 'A';
  if (score >= 80) return 'B';
  if (score >= 70) return 'C';
  if (score >= 60) return 'D';
  return 'F';
};

// Use in cells
spreadsheet.updateCell({ value: '=DOUBLE(5)' }, 'A1');      // 10
spreadsheet.updateCell({ value: '=FTOC(98.6)' }, 'A2');     // 37
spreadsheet.updateCell({ value: '=GRADE(85)' }, 'A3');      // "B"
```

## Placeholders

| Placeholder | Description | Example |
|---|---|---|
| `[HANDLER_NAME]` | Global function name in window scope | `'DoubleHandler'`, `'GradeHandler'` |
| `[FUNCTION_NAME]` | Formula name used in cells (uppercase) | `'DOUBLE'`, `'FTOC'`, `'GRADE'` |
| `[DESCRIPTION]` | User-friendly description | `'Multiplies value by 2'` |

## Notes

- Handler functions must be in global (`window`) scope
- Function names must be uppercase and unique — cannot override built-ins like `SUM`, `AVERAGE`
- Register in the `created` event to ensure spreadsheet is ready
- Custom functions do not persist across page reloads unless re-registered