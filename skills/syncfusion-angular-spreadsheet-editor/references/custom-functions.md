# Custom Functions

Add custom calculation functions to extend the built-in formula engine in the Spreadsheet.

## Table of Contents

- [Key Method](#key-method)
- [Setup](#setup)
- [Minimal Code](#minimal-code)
  - [Component Template](#component-template)
  - [Component Class](#component-class)
- [Placeholders](#placeholders)
- [Notes](#notes)

---

## Key Method

### `addCustomFunction(functionHandler, functionName?, formulaDescription?)`

| Parameter | Type | Required | Description |
|---|---|---|---|
| `functionHandler` | `string \| Function` | ✅ | Global handler name or function reference |
| `functionName` | `string` | ❌ | Formula name used in cells (uppercase) |
| `formulaDescription` | `string` | ❌ | Description shown in formula UI |

**Returns**: `void`

---

## Setup

Install the Syncfusion Spreadsheet package:

```bash
npm install @syncfusion/ej2-angular-spreadsheet
```

Import the module in `app.ts`:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetAllModule, SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [SpreadsheetAllModule],
  template: `<ejs-spreadsheet #spreadsheet></ejs-spreadsheet>`
})
export class AppComponent {
  @ViewChild('spreadsheet') spreadsheet!: SpreadsheetComponent;
}

```

---

## Minimal Code

```typescript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetAllModule, SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [SpreadsheetAllModule],
  template:
  `<ejs-spreadsheet #spreadsheet (created)="onCreated()">
    <e-sheets>
      <e-sheet name="Sheet1"></e-sheet>
    </e-sheets>
  </ejs-spreadsheet>`
})
export class AppComponent {
  @ViewChild('spreadsheet')
  spreadsheet!: SpreadsheetComponent;

  onCreated(): void {
    // Register custom functions
    this.spreadsheet.addCustomFunction('DoubleHandler', 'DOUBLE', 'Multiplies value by 2');
    this.spreadsheet.addCustomFunction('FahrenheitHandler', 'FTOC', 'Fahrenheit to Celsius');
    this.spreadsheet.addCustomFunction('GradeHandler', 'GRADE', 'Returns letter grade');

    // Use in cells
    this.spreadsheet.updateCell({ value: '=DOUBLE(5)' }, 'A1');    // 10
    this.spreadsheet.updateCell({ value: '=FTOC(98.6)' }, 'A2');   // 37
    this.spreadsheet.updateCell({ value: '=GRADE(85)' }, 'A3');    // "B"
  }
}

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
```

---

## Placeholders

| Placeholder | Description | Example |
|---|---|---|
| `[HANDLER_NAME]` | Global function name in window scope | `'DoubleHandler'`, `'GradeHandler'` |
| `[FUNCTION_NAME]` | Formula name used in cells (uppercase) | `'DOUBLE'`, `'FTOC'`, `'GRADE'` |
| `[DESCRIPTION]` | User-friendly description | `'Multiplies value by 2'` |

---

## Notes

- Use `@ViewChild` to access the `SpreadsheetComponent` instance in Angular
- Register custom functions inside the `(created)` event binding to ensure the spreadsheet is fully initialized
- Handler functions must be in global (`window`) scope — place them outside the component class
- Function names must be **uppercase** and unique — cannot override built-ins like `SUM`, `AVERAGE`
- Custom functions do not persist across page reloads unless re-registered
- For better encapsulation, consider registering handlers in a dedicated service or `ngOnInit` lifecycle hook