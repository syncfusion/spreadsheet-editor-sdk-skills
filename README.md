# Syncfusion<sup>®</sup> Spreadsheet Editor SDK Skills

[Spreadsheet Editor SDK](https://www.syncfusion.com/spreadsheet-editor-sdk) skills are specialized instruction sets that teach AI assistants how to perform spreadsheet editor tasks using Syncfusion spreadsheet SDKs (platform-specific editors). These skills follow the [Agent Skills open standard](https://agentskills.io/) and the Agent Skills pattern: each skill includes a `SKILL.md` manifest and topic-level references to guide automated code generation.

## About This Repository

This repository contains **AI-ready skills** focused on spreadsheet editors across multiple platforms (React, Angular, Blazor, ASP.NET Core, TypeScript, Vue, MVC, Windows Forms, WPF). Each skill enables an AI to generate code snippets and provides step-by-step examples.

## Included Platform-Specific Spreadsheet Editor Skills

### Web Frameworks
- [**React Spreadsheet Editor**](./skills/syncfusion-react-spreadsheet-editor/) — Guidance for integrating the Syncfusion React Spreadsheet Editor component into React applications for creating, editing, and managing workbook operations.
- [**Angular Spreadsheet Editor**](./skills/syncfusion-angular-spreadsheet-editor/) — Guidance for integrating the Syncfusion Angular Spreadsheet Editor component into Angular applications.
- [**Blazor Spreadsheet Editor**](./skills/syncfusion-blazor-spreadsheet-editor/) — Guidance for integrating the Syncfusion Blazor Spreadsheet Editor component into Blazor applications.
- [**ASP.NET Core Spreadsheet Editor**](./skills/syncfusion-aspnetcore-spreadsheet-editor/) — Examples and guidance for integrating the Syncfusion Spreadsheet Editor into ASP.NET Core applications (Razor Pages), including server-side import/export workflows and middleware considerations.
- [**ASP.NET MVC Spreadsheet Editor**](./skills/syncfusion-aspnetmvc-spreadsheet-editor/) — Examples and guidance for integrating the Syncfusion Spreadsheet Editor into classic ASP.NET MVC (System.Web.Mvc) projects, including controller action patterns and view helpers.
- [**JavaScript Spreadsheet Editor**](./skills/syncfusion-javascript-spreadsheet-editor/) — Examples and guidance for using the Syncfusion Spreadsheet Editor with JavaScript (ES6) and TypeScript applications.
- [**Vue Spreadsheet Editor**](./skills/syncfusion-vue-spreadsheet-editor/) — Examples and guidance for using the Syncfusion Spreadsheet Editor with Vue applications.

## Getting Started

### How to Integrate Skills

**Step 1: Checkout and copy the required skills**

Clone or download the Spreadsheet-Editor-SDK-Skills repository and copy the skill folders you need (for example: `syncfusion-react-spreadsheet-editor` or `syncfusion-blazor-spreadsheet-editor`) from the `skills/` directory.

**Step 2: Install the skills**

Place the copied skill folders in your workspace following this structure:

```
your-workspace/
├── .github/skills/ or .claude/skills/ or .codestudio/skills/
│   ├── syncfusion-angular-spreadsheet-editor/
│   │   └── SKILL.md
│   ├── syncfusion-aspnetcore-spreadsheet-editor/
│   │   └── SKILL.md
│   ├── syncfusion-aspnetmvc-spreadsheet-editor/
│   │   └── SKILL.md
│   ├── syncfusion-blazor-spreadsheet-editor/
│   │   └── SKILL.md
│   ├── syncfusion-react-spreadsheet-editor/
│   │   └── SKILL.md
│   ├── syncfusion-javascript-spreadsheet-editor/
│   │   └── SKILL.md
│   └── syncfusion-vue-spreadsheet-editor/
│       └── SKILL.md
└── your-project-files...
```

Each skill directory must contain a `SKILL.md` file that defines the skill's behavior.

**Step 3: Verify and manage your skills**

Type `/skills` in the GitHub Copilot or Code Studio chat to quickly access the Configure Skills menu and manage your installed skills.

**Step 4: Use skills**

There are two ways to use skills:

1. **Automatic loading** — Describe your task naturally and the AI agent will load the most relevant skill. Example:

   ```
   Create a spreadsheet with the following data:
   Order ID	Customer Name	Order Date	Address	City	Postal Code	Country	Status	Freight
   10248	Paul Henriot	7/4/1996	59 rue de l'Abbaye	Reims	51100	France	Delivered	$32.38
   10249	Karin Josephs	7/5/1996	Luisenstr. 48	Münster	44087	Germany	Delivered	$11.61

   Apply bold and center for the header row.
   ```

2. **Slash commands** - Type `/` in the GitHub Copilot chat to mention available skills. For example:
   ```
   /react-spreadsheet-editor Create a Spreadsheet with data and apply cell styles
   ```

When a skill is loaded, the AI agent gains specialized knowledge of the Syncfusion Spreadsheet Editor and can help generate code or step-by-step instructions.

## How it works

Each skill supports code generation that produces ready-to-use platform-specific code that can be inserted into your application files (for example, `Program.cs`, `Home.razor`, or `app.ts`). This is ideal when you want to integrate spreadsheet features into your application quickly.

**Trigger keywords:** `create`, `add`, `insert`, `apply`, `snippet`, `how to`, `show me`, `sample`, `example`

## Example Prompts

```
How do I protect Sheet1 and allow only cells in the first and last columns to be edited?
```

### Feature Examples

- Wrap text: "Wrap text in the first column (Customer Name)."
- Number formatting: "Apply currency format to the Amount column."
- Row/Column insert: "Insert a new row at position 5 and hide column C."
- Protection: "Protect Sheet1."
- Chart: "Insert a column chart for Amount by Customer Name."
- Conditional formatting: "Apply conditional formatting to highlight Amounts greater than $15,000 in green."
- Import/Export: "Export the sheet as PDF and CSV."

## References & Resources

- [Syncfusion React Spreadsheet Editor Documentation](https://help.syncfusion.com/document-processing/excel/spreadsheet/react/overview)
- [Syncfusion Angular Spreadsheet Editor Documentation](https://help.syncfusion.com/document-processing/excel/spreadsheet/angular/overview)
- [Syncfusion Blazor Spreadsheet Editor Documentation](https://help.syncfusion.com/document-processing/excel/spreadsheet/blazor/overview)
- [Syncfusion ASP.NET Core Spreadsheet Editor Documentation](https://help.syncfusion.com/document-processing/excel/spreadsheet/asp-net-core/overview)
- [Syncfusion ASP.NET MVC Spreadsheet Editor Documentation](https://help.syncfusion.com/document-processing/excel/spreadsheet/asp-net-mvc/overview)
- [Syncfusion JavaScript Spreadsheet Editor Documentation](https://help.syncfusion.com/document-processing/excel/spreadsheet/javascript-es6/overview)
- [Syncfusion Vue Spreadsheet Editor Documentation](https://help.syncfusion.com/document-processing/excel/spreadsheet/vue/overview)
- [Syncfusion Community License](https://www.syncfusion.com/products/communitylicense)

## License

Syncfusion Spreadsheet Editor require a commercial license for production use. 
[Free Community License](https://www.syncfusion.com/products/communitylicense).
