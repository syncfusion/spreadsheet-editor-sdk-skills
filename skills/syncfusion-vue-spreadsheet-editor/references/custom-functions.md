# Custom Functions

Add custom calculation functions to extend the built-in formula engine in the Spreadsheet Editor.

## Minimal Code

```vue
<template>
  <div class="control-section">
    <ejs-spreadsheet ref="spreadsheet" :created="onCreated">
      <e-sheets>
        <e-sheet :name="Sheet1"></e-sheet>
      </e-sheets>
    </ejs-spreadsheet>
  </div>
</template>

<script>
import {
  SpreadsheetComponent,
  SheetsDirective,
  SheetDirective
} from "@syncfusion/ej2-vue-spreadsheet";

export default {
  components: {
    "ejs-spreadsheet": SpreadsheetComponent,
    "e-sheets": SheetsDirective,
    "e-sheet": SheetDirective
  },

  mounted() {
    // Define global handlers
    window.DoubleHandler = num => num * 2;
    window.GreetHandler = name => `Hello, ${name}!`;
    window.MultiplyHandler = (a, b, c) => a * b * c;
  },

  methods: {
    onCreated() {
      const s = this.$refs.spreadsheet;

      // Register custom formulas
      s.addCustomFunction("DoubleHandler", "DOUBLE", "Multiplies value by 2");
      s.addCustomFunction("GreetHandler", "GREET", "Returns greeting message");
      s.addCustomFunction("MultiplyHandler", "MULTIPLY", "Multiply three numbers");

      // Use formulas
      s.updateCell({ formula: "=SQRT(16)" }, "A1");
      s.updateCell({ formula: "=DOUBLE(5)" }, "A2");
      s.updateCell({ formula: '=GREET("Alice")' }, "A3");
      s.updateCell({ formula: "=MULTIPLY(2,3,4)" }, "A4");
    }
  }
};
</script>

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

```vue
// By function name (string)
spreadsheet.addCustomFunction('MyHandler', 'MYFUNCTION', 'My custom function');

// By function reference (less common)
spreadsheet.addCustomFunction((num: number) => num * 2, 'DOUBLE');
```

## Implementation Patterns

### Simple Single-Parameter Function
```vue
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
```vue
spreadsheet.addCustomFunction('TemperatureHandler', 'FTOC', 'Convert Fahrenheit to Celsius');

window.TemperatureHandler = (fahrenheit) => {
  return (fahrenheit - 32) * (5 / 9);
};

spreadsheet.updateCell({ formula: '=FTOC(98.6)' }, 'C1'); // Result: 37
```

### Function with Multiple Inputs
```vue
spreadsheet.addCustomFunction('CompoundHandler', 'COMPOUND', 'Calculate compound interest');

window.CompoundHandler = (principal, rate, time) => {
  // A = P * (1 + r/100)^t
  return principal * Math.pow(1 + rate / 100, time);
};

spreadsheet.updateCell({ value: '=COMPOUND(1000, 5, 2)' }, 'D1'); // Result: 1102.5
```

### Function with Text Output
```vue
spreadsheet.addCustomFunction('GradeHandler', 'GRADE', 'Assign letter grade');

window.GradeHandler = (score) => {
  if (score >= 90) return 'A';
  if (score >= 80) return 'B';
  if (score >= 70) return 'C';
  if (score >= 60) return 'D';
  return 'F';
};

spreadsheet.updateCell({ formula: '=GRADE(85)' }, 'E1'); // Result: "B"
```

### Function Referencing Cell Values
```vue
spreadsheet.addCustomFunction('SumSquaresHandler', 'SUMSQ', 'Sum of squares of two numbers');

window.SumSquaresHandler = (a, b) => {
  return (a * a) + (b * b);
};

// Use with cell references
spreadsheet.updateCell({ formula: '=SUM(A1:A10)' }, 'A11');
spreadsheet.updateCell({ formula: '=SUMSQ(5, 3)' }, 'A12');        // Result: 34
spreadsheet.updateCell({ formula: '=SUMSQ(A11, 10)' }, 'A13');    // A11=value, static 10
```

### Function with Array/Range Input (Advanced)
```vue
spreadsheet.addCustomFunction('MaxDiffHandler', 'MAXDIFF', 'Max difference in range');

window.MaxDiffHandler = (range) => {
  if (!range || range.length === 0) return 0;
  const max = Math.max(...range);
  const min = Math.min(...range);
  return max - min;
};

```

### Namespace Prefix for Organization
```vue
// Add multiple related functions with namespace prefix
spreadsheet.addCustomFunction('MATH_ABSHandler', 'MATH_ABS', 'Absolute value');
spreadsheet.addCustomFunction('MATH_POWHandler', 'MATH_POW', 'Power function');
spreadsheet.addCustomFunction('MATH_SQRTHandler', 'MATH_SQRT', 'Square root');

window.MATH_ABSHandler = (num) => Math.abs(num);
window.MATH_POWHandler = (base, exp) => Math.pow(base, exp);
window.MATH_SQRTHandler = (num) => Math.sqrt(num);

spreadsheet.updateCell({ formula: '=MATH_ABS(-5)' }, 'A1');      // 5
spreadsheet.updateCell({ formula: '=MATH_POW(2, 3)' }, 'A2');    // 8
spreadsheet.updateCell({ formula: '=MATH_SQRT(16)' }, 'A3');     // 4
```

### Function with Error Handling
```vue
spreadsheet.addCustomFunction('SafeDivideHandler', 'SAFEDIV', 'Divide with error handling');

window.SafeDivideHandler = (numerator, denominator) => {
  if (denominator === 0) {
    return '#DIV/0!';  // Excel-style error
  }
  return numerator / denominator;
};

spreadsheet.updateCell({ formula: '=SAFEDIV(10, 2)' }, 'B1');    // 5
spreadsheet.updateCell({ formula: '=SAFEDIV(10, 0)' }, 'B2');    // "#DIV/0!"
```

### Function with Conditional Logic
```vue
spreadsheet.addCustomFunction('DiscountHandler', 'DISCOUNT', 'Apply discount based on amount');

window.DiscountHandler = (amount, tier) => {
  let discount = 0;
  if (tier === 1) discount = 0.05;        // 5% for tier 1
  else if (tier === 2) discount = 0.10;   // 10% for tier 2
  else if (tier === 3) discount = 0.15;   // 15% for tier 3
  
  return amount * (1 - discount);
};

spreadsheet.updateCell({ formula: '=DISCOUNT(100, 2)' }, 'C1');  // 90 (10% discount)
```

## Advanced: Function Registration at Initialization

```vue
<template>
<div class="control-section">
  <ejs-spreadsheet ref="spreadsheet" :created="onCreated">
    <e-sheets>
      <e-sheet :name="Sheet1"></e-sheet>
    </e-sheets>
  </ejs-spreadsheet>
</div>
</template>

<script>
import {
SpreadsheetComponent,
SheetsDirective,
SheetDirective
} from "@syncfusion/ej2-vue-spreadsheet";

export default {
components: {
  "ejs-spreadsheet": SpreadsheetComponent,
  "e-sheets": SheetsDirective,
  "e-sheet": SheetDirective
},

mounted() {
  // Global handlers
  window.SQRTHandler = num => Math.sqrt(num);
  window.CubeHandler = num => num ** 3;
  window.RectAreaHandler = (length, width) => length * width;
},

methods: {
  onCreated() {
    const s = this.$refs.spreadsheet;

    // Array of custom functions
    const customFns = [
      { handler: "SQRTHandler", name: "SQRT", desc: "Square root" },
      { handler: "CubeHandler", name: "CUBE", desc: "Cube value" },
      { handler: "RectAreaHandler", name: "RECTAREA", desc: "Rectangle area" }
    ];

    // Register all custom functions
    customFns.forEach(fn => {
      s.addCustomFunction(fn.handler, fn.name, fn.desc);
    });
  }
}
};
</script>
```

## Naming Conventions

| Pattern | Example | Use Case |
|---------|---------|----------|
| Functional | `SQRT`, `CONVERT`, `CALCULATE` | General utilities |
| Namespace | `MATH_ABS`, `TEXT_UPPER`, `DATE_NOW` | Related function groups |
| Domain | `SALES_TAX`, `PAYROLL_TAX`, `DISCOUNT` | Business-specific |
| Prefixed | `CUSTOM_SQRT`, `USER_GRADE` | User-defined vs built-in |

## Notes

- **Best Practice**: Use UPPERCASE for custom function names (follows Excel convention)
- **Best Practice**: Handler functions must be globally accessible (`window` scope)
- **Best Practice**: Use namespace prefixes to avoid conflicts (`CUSTOM_`, `APP_`, `BIZ_`)
- **Best Practice**: Add descriptions to help users understand function purpose
- **Performance**: Custom functions run on the client; avoid heavy computations
- **Limitation**: Array/range parameters may not be supported directly; pass individual cells instead

## Testing Custom Functions

```vue
// Test directly in TypeScript
const result1 = window.SQRTHandler(16);
console.log(`SQRT(16) = ${result1}`);  // 4

const result2 = window.DoubleHandler(5);
console.log(`DOUBLE(5) = ${result2}`);  // 10

// Test via formula in spreadsheet
spreadsheet.updateCell({ formula: '=SQRT(25)' }, 'A1');
spreadsheet.updateCell({ formula: '=DOUBLE(10)' }, 'A2');
```
