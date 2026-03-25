# Custom Functions

Add custom calculation functions to extend the built-in formula engine in the Spreadsheet Editor.

## Minimal Code

```jsx
import * as React from 'react';
import { SheetsDirective, SheetDirective } from '@syncfusion/ej2-react-spreadsheet';
import { SpreadsheetComponent } from '@syncfusion/ej2-react-spreadsheet';

function Default() {
    const spreadsheetRef = React.useRef(null);
    
    // === Define the handler functions (global scope) ===
    window.DoubleHandler = (num) => {
      return num * 2;
    };

    window.GreetHandler = (name) => {
      return `Hello, ${name}!`;
    };

    window.MultiplyHandler = (a, b, c) => {
      return a * b * c;
    };
    //Bind created event to perform the action during initial load.
    const onCreated = () => {
      const spreadsheet = spreadsheetRef.current; 
      // === Add custom function ===
      // addCustomFunction(functionHandler, functionName?, formulaDescription?)
      
      // Add custom DOUBLE function
      spreadsheet.addCustomFunction('DoubleHandler', 'DOUBLE', 'Multiplies value by 2');
      
      // Add custom GREET function
      spreadsheet.addCustomFunction('GreetHandler', 'GREET', 'Returns greeting message');

      // === Custom function with multiple parameters ===
      spreadsheet.addCustomFunction('MultiplyHandler', 'MULTIPLY', 'Multiply three numbers');

      // === Use in formulas ===
      spreadsheet.updateCell({ formula: '=SQRT(16)' }, 'A1');        // Result: 4
      spreadsheet.updateCell({ formula: '=DOUBLE(5)' }, 'A2');        // Result: 10
      spreadsheet.updateCell({ formula: '=GREET("Alice")' }, 'A3');   // Result: "Hello, Alice!"
      spreadsheet.updateCell({ formula: '=MULTIPLY(2, 3, 4)' }, 'A4'); // Result: 24
    }
    return (<SpreadsheetComponent ref={spreadsheetRef} created={onCreated}>
                    <SheetsDirective>
                        <SheetDirective name="Sheet1">
                        </SheetDirective>
                    </SheetsDirective>
                </SpreadsheetComponent>);}
export default Default;
```

## Placeholders

| Placeholder | Description | Example |
|---|---|---|
| `[HANDLER_NAME]` | Global function name (window scope) | `'CalculateHandler'`, `'ConvertHandler'` |
| `[FUNCTION_NAME]` | Formula function name (uppercase) | `'SQRT'`, `'DOUBLE'`, `'MULTIPLY'` |
| `[DESCRIPTION]` | User-friendly description | `'Calculates square root'`, `'Converts F to C'` |
| `[PARAM1], [PARAM2]` | Function parameters | `num`, `value`, `celsius` |

## Key Methods

### `addCustomFunction(functionHandler, functionName?, formulaDescription?)`
Registers a custom function for use in formulas.

**Parameters**:
- `functionHandler` (string | Function) — handler function name or reference
- `functionName` (string, optional) — formula function name (default: handler name)
- `formulaDescription` (string, optional) — description for UI

**Returns**: void

```jsx
// By function name (string)
spreadsheet.addCustomFunction('MyHandler', 'MYFUNCTION', 'My custom function');

```

## Implementation Patterns

### Simple Single-Parameter Function
```jsx
// Add to created event or after initialization
spreadsheet.addCustomFunction('InchesToCmHandler', 'INTOCM', 'Convert inches to centimeters');

// Define handler globally
window.InchesToCmHandler = (inches) => {
  return inches * 2.54;
};
// Use in formula
spreadsheet.updateCell({ formula: '=INTOCM(10)' }, 'B1'); // Result: 25.4
```

### Multi-Parameter Function
```jsx
spreadsheet.addCustomFunction('TemperatureHandler', 'FTOC', 'Convert Fahrenheit to Celsius');

window.TemperatureHandler = (fahrenheit) => {
  return (fahrenheit - 32) * (5 / 9);
};

spreadsheet.updateCell({ formula: '=FTOC(98.6)' }, 'C1'); // Result: 37
```

## Notes
- Handler functions must be globally accessible (`window` scope)
- Use namespace prefixes to avoid conflicts (`CUSTOM_`, `APP_`, `BIZ_`)
- Custom functions are stored at the workbook level — won't persist across page reloads.
- Function names must be unique (even from built-in functions like SUM, AVERAGE)
- Custom functions run on the client; avoid heavy computations
- Array/range parameters may not be supported directly; pass individual cells instead

