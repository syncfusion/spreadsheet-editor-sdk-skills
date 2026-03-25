# Initialization & Basic Rendering

Create and render the Syncfusion Spreadsheet Editor component — the starting point for any spreadsheet integration.

## Installation

Before generating code, ensure the required npm package is installed. If the workspace contains an existing React project and does not already have `@syncfusion/ej2-spreadsheet` installed, run the following command:
```bash
npm install @syncfusion/ej2-spreadsheet --save
```
**Note:** Do not execute this installation if the workspace does not contain any project (i.e., no `package.json` file exists).

## Minimal Code

```typescript
import { Spreadsheet } from '@syncfusion/ej2-spreadsheet';

// Create spreadsheet instance
const spreadsheet = new Spreadsheet({
  // Initial sheet configuration (at least one sheet required)
  sheets: [
    {
      name: 'Sheet1',
      // Optional: initial data (array of objects)
      ranges: [
        {
          dataSource: [
            { Product: 'Laptop', Price: 1200, Quantity: 5 },
            { Product: 'Mouse', Price: 25, Quantity: 20 },
            { Product: 'Keyboard', Price: 80, Quantity: 10 }
          ],
          // Optional: start cell for data (default A1)
          startCell: 'A1'
        }
      ]
    }
  ]
});

// Render into DOM element
spreadsheet.appendTo('#spreadsheet'); // <div id="spreadsheet"></div> must exist in HTML

// Add formulas after rendering (dataSource does not evaluate formula strings)
spreadsheet.updateCell({ value: '=B2*C2' }, 'D2');
spreadsheet.updateCell({ value: '=B3*C3' }, 'D3');
spreadsheet.updateCell({ value: '=B4*C4' }, 'D4');
```

## Placeholders

| Placeholder | Description | Example |
|---|---|---|
| `[SHEET_NAME]` | Sheet name | `'Sheet1'`, `'Sales'` |
| `[DATA_SOURCE]` | Initial data — plain values only, no formulas | `[{ Product: 'Laptop' }]` |
| `[START_CELL]` | Data start cell | `'A1'`, `'A2'` |
| `[CONTAINER_ID]` | HTML element ID | `'#spreadsheet'` |
---

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
@import '../node_modules/@syncfusion/ej2-grids/styles/bootstrap5.css';
@import '../node_modules/@syncfusion/ej2-spreadsheet/styles/bootstrap5.css';

## Notes
- Include container div with height
- Container must exist before render to the DOM