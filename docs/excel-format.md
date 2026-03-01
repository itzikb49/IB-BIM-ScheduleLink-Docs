# Excel File Format

## Overview

ScheduleLink uses a structured Excel format (.xlsx) to transfer data between Revit and Excel. This document describes the file structure in detail.

---

## File Structure

Each exported file contains two worksheets:

### 1. Data Sheet

Named after the Revit schedule (e.g., "Sheet List", "Room Schedule").

**Row 1** — Header row with parameter names (green background)

**Row 2+** — Data rows, one per Revit element

**Column A** — Element ID (unique Revit identifier)

**Columns B+** — Parameter values

### 2. Instructions Sheet

Contains metadata:

| Row | Column A | Column B |
|-----|----------|----------|
| 1 | Schedule Name | *(name)* |
| 2 | Schedule ID | *(Revit element ID)* |
| 3 | Export Date | *(date and time)* |
| 4 | Revit Version | *(version name)* |
| 5 | Rows | *(count)* |
| 6 | Columns | *(count)* |

---

## Column Color Coding

### Header Row (Row 1)

All headers have a **green background** with white text and auto-filter enabled.

### Data Rows (Row 2+)

| Cell Background | Meaning | Import Behavior |
|----------------|---------|-----------------|
| **White** | Editable parameter | ✅ Changes will be applied |
| **Pink** (`#FFC7CE`) | Read-only parameter | ⛔ Changes will be ignored |
| **Gray** (`#D9D9D9`) | Read-only parameter | ⛔ Changes will be ignored |

---

## Element ID Column

The **Element ID** column is critical for import:

- Contains the unique Revit element identifier
- Used to match Excel rows to Revit elements
- **Must not be modified, deleted, or rearranged**
- If an Element ID is missing or invalid, the row is skipped during import

---

## Supported Data Types

| Revit Parameter Type | Excel Format | Import Notes |
|---------------------|-------------|--------------|
| **Text** | Plain text | Imported as-is |
| **Integer** | Number | Must be a whole number |
| **Number (Double)** | Number | Decimal separator: period (.) or local format |
| **Yes/No** | Text | Accepts: "Yes"/"No", "1"/"0", "True"/"False", "כן"/"לא" |
| **Element ID** | Number | Must be a valid element ID |
| **Length** | Number | Automatically converted to internal units |

---

## Formatting Details

The exported Excel file includes professional formatting:

- **Auto-fit column widths** — Columns adjust to content width
- **Borders** — Thin borders around all cells for readability
- **Frozen header** — Row 1 is frozen for easy scrolling
- **Auto-filter** — Filter dropdowns on all header columns

---

## Rules for Editing

### ✅ Do

- Edit values in **white** columns only
- Keep the Element ID column intact
- Save as .xlsx format
- Use correct data types for each parameter

### ❌ Don't

- Delete or modify the Element ID column
- Add or remove rows
- Add or remove columns
- Rename the data sheet
- Change column order
- Save as .csv or .xls (use .xlsx only)

---

## Working with Multiple Schedules

Each export creates a separate Excel file. To update multiple schedules:

1. Export each schedule to its own file
2. Edit each file separately
3. Import each file back one at a time

> **Note:** Each Excel file is linked to a specific schedule via the Schedule ID stored in the Instructions sheet.
