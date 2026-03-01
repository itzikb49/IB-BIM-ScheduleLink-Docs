# ScheduleLink for Autodesk Revit

<div align="center">

**Export and Import Revit Schedules to Excel — Edit, Update, and Sync Back**

[![Revit 2023](https://img.shields.io/badge/Revit-2023-blue)]()
[![Revit 2024](https://img.shields.io/badge/Revit-2024-blue)]()
[![Revit 2025](https://img.shields.io/badge/Revit-2025-blue)]()
[![Revit 2026](https://img.shields.io/badge/Revit-2026-blue)]()

*By [IB-BIM](https://github.com/itzikb49)*

</div>

---

## Overview

**ScheduleLink** bridges Revit schedules and Excel. Export any schedule to a formatted Excel file, make your changes, and import them back — all parameter updates are applied directly to the Revit elements.

### Key Features

- **One-Click Export** — Any Revit schedule to formatted Excel with color-coded columns
- **Smart Import** — Edit values in Excel and sync back to Revit with full validation
- **Sheet Number Safety** — Two-pass algorithm prevents conflicts when renaming sheets
- **Duplicate Detection** — Identifies duplicate unique values before applying changes
- **Error Resilience** — Failed rows don't cancel the entire operation
- **Detailed Results** — Clear report showing updated, skipped, unchanged, and failed items
- **Undo Support** — Single transaction means Ctrl+Z reverts all changes
- **Multi-Version** — Supports Revit 2023, 2024, 2025, and 2026

---

## Documentation

| Document | Description |
|----------|-------------|
| [Getting Started](docs/getting-started.md) | Installation and first use |
| [Export Guide](docs/export-guide.md) | How to export schedules to Excel |
| [Import Guide](docs/import-guide.md) | How to import changes from Excel |
| [Excel Format](docs/excel-format.md) | Understanding the Excel file structure |
| [Error Handling](docs/error-handling.md) | Understanding errors and how to resolve them |
| [FAQ](docs/faq.md) | Frequently asked questions |

---

## Quick Start

1. **Export** — Select a schedule → Click Export → Save Excel file
2. **Edit** — Open in Excel → Modify editable (white) columns → Save
3. **Import** — Click Import → Select the Excel file → Review results

> **Tip:** Read-only columns are marked with a pink/gray background in Excel. Do not modify them — changes will be ignored.

---

## System Requirements

- Autodesk Revit 2023, 2024, 2025, or 2026
- Windows 10/11
- Microsoft Excel (for editing exported files)

---

## Support

For issues or feature requests, please open an [Issue](https://github.com/itzikb49/ScheduleLink-Docs/issues).

---

## License

This software is available on the [Autodesk App Store](https://apps.autodesk.com/).

© 2026 IB-BIM. All rights reserved.
