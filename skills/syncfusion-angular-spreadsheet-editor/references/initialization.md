# Initialization & Basic Rendering

Create and render the Syncfusion Spreadsheet component in Angular.

## Installation

Before generating code, ensure the required npm package is installed. If the workspace contains an existing Angular project and does not already have `@syncfusion/ej2-angular-spreadsheet` installed, run the following command:

```bash
npm install @syncfusion/ej2-angular-spreadsheet --save
```
**Note:** Do not execute this installation if the workspace does not contain any project (i.e., no `package.json` file exists).

## Minimal Angular Code

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
      <e-sheet name="Sheet1">
        <e-ranges>
          <e-range [dataSource]="data" startCell="A1"></e-range>
        </e-ranges>
      </e-sheet>
    </e-sheets>
  </ejs-spreadsheet>`
})
export class AppComponent {
  @ViewChild('spreadsheet') spreadsheet!: SpreadsheetComponent;

  data: object[] = [
    { Product: 'Laptop',   Price: 1200, Quantity: 5  },
    { Product: 'Mouse',    Price: 25,   Quantity: 20 },
    { Product: 'Keyboard', Price: 80,   Quantity: 10 }
  ];

  onCreated(): void {
    // Formulas must use updateCell() — formula strings in dataSource are treated as plain text
    this.spreadsheet.updateCell({ formula: '=B2*C2' }, 'D2');
    this.spreadsheet.updateCell({ formula: '=B3*C3' }, 'D3');
    this.spreadsheet.updateCell({ formula: '=B4*C4' }, 'D4');
  }
}
```

## API Reference

### Sheet Initialization Properties

| Property | Type | Description | Example |
|---|---|---|---|
| `name` | `string` | Sheet tab name | `'Sheet1'`, `'Sales'` |
| `[dataSource]` | `object[]` | Bind data — plain values only, no formulas | `[{ Product: 'Laptop' }]` |
| `startCell` | `string` | Cell where data binding starts | `'A1'`, `'B2'` |

### updateCell(cell, address)

| Parameter | Type | Description | Example |
|---|---|---|---|
| `value` | `string` | Plain text or number | `'Laptop'`, `1200` |
| `formula` | `string` | Formula string | `'=B2*C2'` |
| `address` | `string` | Target cell address | `'D2'` |

### Key Feature Flags

| Property | Type | Default | Description |
|---|---|---|---|
| `[enableFormula]` | `boolean` | `true` | Enable formula parsing and calculation |
| `[allowEditing]` | `boolean` | `true` | Allow cell editing |
| `[showRibbon]` | `boolean` | `true` | Show ribbon toolbar |
| `[showSheetTabs]` | `boolean` | `true` | Show sheet tabs |
| `[showFormulaBar]` | `boolean` | `true` | Show formula bar |

## Notes

- Container must have a **fixed height** (e.g., `height: 600px`) — component needs explicit height to render
- Formula strings in `dataSource` are treated as **plain text** — use `updateCell({ formula: '...' })` inside `(created)` event instead
- `(created)` event fires once after the component fully renders — always use it for post-init operations
- All features are **enabled by default** — only set feature flags when explicitly disabling

## CSS Imports

**Important:** Add the following CSS imports when the current workspace app/project does not already load Syncfusion styles globally. Place them in the project's global stylesheet before rendering the Spreadsheet component.

If your project already imports the same Syncfusion theme styles elsewhere, do not duplicate them.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-lists/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-spreadsheet/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-grids/styles/bootstrap5.css';
```

## Notes for CSS
- Include container div with height
- Container must exist before render to the DOM