# Initialization & Basic Rendering

Create and render the Syncfusion Spreadsheet Editor component — the starting point for any spreadsheet integration.

## Installation
 
Before generating code, ensure the required npm package is installed. If the workspace contains an existing React project and does not already have `@syncfusion/ej2-vue-spreadsheet` installed, run the following command:
```bash
npm install @syncfusion/ej2-vue-spreadsheet --save
```
**Note:** Do not execute this installation if the workspace does not contain any project (i.e., no `package.json` file exists).

## Minimal Code

```vue
<template>
<div class="control-section">
  <ejs-spreadsheet
    ref="spreadsheet"
    openUrl="https://document.syncfusion.com/web-services/spreadsheet-editor/api/spreadsheet/open"
    saveUrl="https://document.syncfusion.com/web-services/spreadsheet-editor/api/spreadsheet/save"
  >
    <e-sheets>
      <e-sheet name="Sheet1">
        <e-ranges>
          <e-range :dataSource="defaultData" />
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
  defaultData: [
    { Product: "Laptop", Price: 1200, Quantity: 5, Total: "=B2*C2" },
    { Product: "Mouse", Price: 25, Quantity: 20, Total: "=B3*C3" },
    { Product: "Keyboard", Price: 80, Quantity: 10, Total: "=B4*C4" }
  ]
})
};
</script>
```
## Placeholders
| Placeholder | Description | Example |
|---|---|---|
| [FEATURE_FLAGS] | Disable features (only add if false) | allowEditing={false} |
| [SHEET_NAME] | Sheet name | 'Sheet1', 'Sales' |
| [DATA_SOURCE] | Initial data | [{Product: 'Laptop'}] |
| [START_CELL] | Data start | 'A1', 'A2' |
| [CONTAINER_ID] | HTML element ID | 'sample' |

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
@import '../node_modules/@syncfusion/ej2-vue-spreadsheet/styles/bootstrap5.css';
```

## Notes
- Include container div with height
- Container must exist before render to the DOM
