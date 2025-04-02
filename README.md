


# XGSL (eXtensible Grid Sheet Language)  

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Build Status](https://github.com/your-username/xgsl/actions/workflows/ci.yml/badge.svg)](https://github.com/your-username/xgsl/actions)
[![Rust Version](https://img.shields.io/badge/Rust-1.70%2B-orange)](https://www.rust-lang.org)

**Spreadsheets as Code.** Define complex spreadsheets declaratively, version them with Git, and export to Excel, Google Sheets, or LibreOffice.

```java
// Example: Sales Report
@compose(Product, Sales)
table SalesReport {
  @label("Product") @style(bold)
  name: Product.name

  @label("Revenue") @style(currency)
  revenue: Formula(Sales.units * Product.price)
}
```

## Features ✨

- **Declarative Syntax** – Define tables, formulas, and styles in code.
- **Export Everywhere** – Compile to `.xlsx`, Google Sheets, or `.ods`.
- **Version Control** – Human-readable diffs (unlike binary `.xlsx` files).
- **IDE Support** – Autocomplete, diagnostics, and hover docs via LSP.
- **Template Reuse** – Inherit and compose spreadsheets with `@import`.

## Quick Start 🚀

### Install the CLI
```bash
cargo install xgsl
```

### Compile a Spreadsheet
```bash
xgsl compile report.xgsl --target excel
```

### Format Your Code
```bash
xgsl fmt report.xgsl
```

## Language Highlights

### Formulas with Virtual Variables
```java
// Relative references (like Excel’s A1 notation, but readable)
growth: Formula((.up.revenue - this.revenue) / .up.revenue)
```

### Cross-Entity References
```java
// Pull data from other tables
inventory: Formula(Inventory[this.product_id].stock)
```

### Dependency Management
```java
// Import templates from GitHub
@import("github:company/report-templates@v1.2")
table Q4Report extends QuarterlyTemplate { ... }
```

## Roadmap 🗺️

| Feature               | Status       |
|-----------------------|-------------|
| Excel Exporter        | ✅ Released  |
| Google Sheets Exporter| 🚧 In Progress |
| Language Server (LSP) | 🔜 Planned   |
| Dependency Resolver   | 🔜 Planned   |

## Contributing 🤝

We welcome contributions! See:
- [RFC 0001](rfcs/0001-xgsl.md) – Design overview.
- [CONTRIBUTING.md](CONTRIBUTING.md) – Development guidelines.

## Why XGSL?

| Problem               | XGSL Solution              |
|-----------------------|----------------------------|
| Manual edits break logic | Spreadsheets defined as code |
| Unreadable Git diffs   | Clean, versionable syntax   |
| No template reuse      | `@import` and inheritance  |

---

📌 **Star this repo** to stay updated!  
💬 **Questions?** Open a GitHub Discussion.
```

---

### Key Design Choices:
1. **Visual Appeal** – Shields, emojis, and tables make it skimmable.  
2. **Problem/Solution** – Clearly contrasts XGSL with traditional spreadsheets.  
3. **Action-Oriented** – Quick start section gets users coding immediately.  
4. **Transparency** – Roadmap builds trust in project maturity.  
