---
layout: default
title: "ScheduleLink — User Guide"
---

[← Back to Home](index.md)

# 📖 IB-BIM ScheduleLink — User Guide

<p align="center">
  <img src="Images/IB-BIM_200X200.png" alt="IB-BIM Logo" width="120">
</p>

---

## Table of Contents

- [1. Overview](#1-overview)
- [2. Installation](#2-installation)
- [3. The Main Dialog](#3-the-main-dialog)
- [4. Exporting a Schedule](#4-exporting-a-schedule)
- [5. Understanding the Excel File](#5-understanding-the-excel-file)
- [6. Editing in Excel](#6-editing-in-excel)
- [7. Importing Changes](#7-importing-changes)
- [8. Import Results Dialog](#8-import-results-dialog)
- [9. Sheet Number Handling](#9-sheet-number-handling)
- [10. Supported Data Types](#10-supported-data-types)
- [11. Error Handling](#11-error-handling)
- [12. Log Files](#12-log-files)
- [13. Tips and Best Practices](#13-tips-and-best-practices)
- [14. Uninstallation](#14-uninstallation)

---

## 1. Overview

**ScheduleLink** is a Revit add-in that creates a live bridge between Revit schedules and Excel. It allows you to:

- Export any Revit schedule to a professionally formatted Excel file
- Edit parameter values in the familiar Excel environment
- Import changes back into Revit with full validation
- Handle unique parameters (like Sheet Numbers) safely

All changes are applied in a **single Revit transaction**, so you can undo everything with **Ctrl+Z**.

---

## 2. Installation

### From the Autodesk App Store

1. Visit the [Autodesk App Store](https://apps.autodesk.com/) and search for **ScheduleLink**
2. Download the installer for your Revit version
3. Close all running Revit instances
4. Run the installer and follow the prompts
5. Launch Revit

### Verifying Installation

After launching Revit, go to the **Add-Ins** tab. You should see the **ScheduleLink** button in the ribbon.

If the button does not appear:
- Ensure Revit was fully closed before installation
- Check that your Revit version is supported (2023–2026)
- Try restarting your computer

### Supported Versions

| Revit Version | Status |
|---------------|--------|
| Revit 2023 | ✅ Supported |
| Revit 2024 | ✅ Supported |
| Revit 2025 | ✅ Supported |
| Revit 2026 | ✅ Supported |

---

## 3. The Main Dialog

Click the **ScheduleLink** button in the Add-Ins tab to open the main dialog.

### Layout

The dialog is divided into two panels:

**Left Panel — Schedule List**
- Displays all schedules in the current Revit project
- **Search box** at the top filters schedules by name in real-time
- Shows the total count of schedules found
- Click any schedule to select it

**Right Panel — Parameter Preview**
- Shows all parameters of the selected schedule
- Each parameter is color-coded by editability:

| Color | Meaning |
|-------|---------|
| 🟢 **Green** | Editable — can be modified via Import |
| 🔴 **Red / Pink** | Read-only — exported for reference only |
| 🟡 **Yellow** | Calculated — cannot be modified |

**Bottom Bar**
- **Export** button — exports the selected schedule to Excel
- **Import** button — imports changes from an Excel file

### Search

Type in the search box to filter schedules by name. The list updates instantly as you type. Clear the search box to show all schedules again.

---

## 4. Exporting a Schedule

### Step-by-Step

1. **Select a schedule** from the left panel
2. Review the parameter preview in the right panel
3. Click **Export**
4. Choose a save location and filename in the Save dialog
5. Wait for the progress bar to complete

### What Gets Exported

- **All elements** in the schedule, including those hidden by filters
- **All parameters** shown in the schedule view
- **Element IDs** — a hidden column used to match rows during import
- **Metadata** — schedule name, ID, export date, and Revit version (in the Instructions sheet)

### Export Progress

A progress bar shows real-time export progress. For large schedules (1000+ rows), export may take several seconds.

---

## 5. Understanding the Excel File

The exported file contains **two worksheets**:

### Data Sheet

Named after the Revit schedule (e.g., "Sheet List", "Room Schedule").

| Column | Description |
|--------|-------------|
| **A — Element ID** | Unique Revit element identifier. **Do not modify.** |
| **B, C, D...** | Schedule parameters in the order they appear in Revit |

### Instructions Sheet

Contains export metadata:

| Field | Description |
|-------|-------------|
| Schedule Name | Name of the exported schedule |
| Schedule ID | Revit element ID of the schedule view |
| Export Date | Date and time of export |
| Revit Version | Version of Revit used |
| Row Count | Number of data rows |
| Column Count | Number of parameter columns |

### Column Colors

| Cell Background | Meaning | Import Behavior |
|----------------|---------|-----------------|
| **White** | Editable parameter | ✅ Changes will be applied |
| **Pink** | Read-only parameter | ⛔ Changes will be ignored |
| **Gray** | Read-only parameter | ⛔ Changes will be ignored |

### Formatting

The Excel file includes professional formatting:
- Green header row with white text and auto-filter
- Auto-fit column widths
- Thin borders around all cells
- Frozen header row for easy scrolling

---

## 6. Editing in Excel

### Rules for Safe Editing

**✅ Do:**
- Edit values only in **white** (editable) columns
- Keep the Element ID column (column A) intact
- Save as **.xlsx** format
- Use correct data types for each parameter
- Close the file before importing

**❌ Don't:**
- Delete or modify the Element ID column
- Add or remove rows
- Add or remove columns
- Rename the data sheet
- Change column order
- Save as .csv or .xls

### Data Type Reference

| Parameter Type | How to Enter |
|---------------|-------------|
| Text | Type any text value |
| Number (Integer) | Enter a whole number (e.g., `42`) |
| Number (Decimal) | Use period as separator (e.g., `3.14`) |
| Yes/No | Enter `Yes` / `No`, `1` / `0`, `True` / `False`, or `כן` / `לא` |
| Length | Enter the numeric value (automatic unit conversion) |

---

## 7. Importing Changes

### Step-by-Step

1. Click **Import** in the ScheduleLink dialog
2. Select the modified Excel file
3. Wait for the progress bar to complete
4. Review the results dialog

### What Happens During Import

1. ScheduleLink reads the Excel file and validates the data
2. All parameters are updated element by element
3. A single Revit transaction is committed
4. The results dialog shows a complete summary

### Undo

All changes are wrapped in a **single Revit transaction**. Press **Ctrl+Z** in Revit to undo all changes at once.

> ⚠️ Undo works only before saving the Revit file. After saving, changes are permanent.

---

## 8. Import Results Dialog

After every import, a results dialog shows:

```
Rows: 23
Updated: 21
Unchanged: 115
Read-only (skipped): 0
Not found: 0
Failed: 2

Errors:
  Row 10: Excel value 'ABC-123' is duplicate → kept Revit value 'ABC-123'
  Row 24: Excel value 'ABC-123' is duplicate → kept Revit value 'DEF-456'
```

### Field Descriptions

| Field | Description |
|-------|-------------|
| **Rows** | Total data rows in the Excel file |
| **Updated** | Parameter values successfully changed |
| **Unchanged** | Values identical to Revit (no change needed) |
| **Read-only (skipped)** | Edits in read-only columns (ignored) |
| **Not found** | Elements with invalid or missing Element IDs |
| **Failed** | Values that could not be applied (with details) |

### Error Messages

If errors occurred, they are listed with:
- **Row number** — corresponding to the Excel row
- **Error description** — what went wrong
- **Action taken** — what ScheduleLink did to recover

---

## 9. Sheet Number Handling

### Renaming Sheets

You can freely rename Sheet Numbers in Excel — including swapping numbers between sheets. ScheduleLink handles all scenarios automatically without conflicts.

### Duplicate Detection

ScheduleLink checks for duplicate Sheet Numbers **before** applying changes. If duplicates are found:

- The duplicate values are **not applied**
- The original Revit values are **restored** for the affected rows
- A clear error message is shown in the results dialog
- All non-duplicate changes proceed normally

### Example

If your Excel file contains two rows with the same Sheet Number `ABC-01`:

| Row | Excel Value | Result |
|-----|------------|--------|
| 10 | ABC-01 | ⛔ Not applied — restored to original Revit value |
| 12 | ABC-01 | ⛔ Not applied — restored to original Revit value |

> 💡 **Tip:** Use Excel's `COUNTIF` formula to find duplicates before importing:  
> `=COUNTIF(B:B, B2)` — values greater than 1 indicate duplicates.

---

## 10. Supported Data Types

ScheduleLink handles all standard Revit parameter types:

| Revit Type | Storage | Import Format |
|-----------|---------|--------------|
| **Text** | String | Any text value |
| **Integer** | Integer | Whole number |
| **Number** | Double | Decimal number (period or local separator) |
| **Yes/No** | Integer | "Yes"/"No", "1"/"0", "True"/"False", "כן"/"לא" |
| **Length** | Double | Numeric value (auto-converted to internal units) |
| **Area** | Double | Numeric value (auto-converted to internal units) |
| **Element ID** | ElementId | Valid element ID number |

### Unit Conversion

For parameters with units (length, area, volume), ScheduleLink automatically converts between display units and Revit's internal units. Enter values as they appear in the schedule — the conversion is handled automatically.

---

## 11. Error Handling

### Design Philosophy

ScheduleLink is designed for **resilience**:
- A single error does **not** cancel the entire operation
- Successful changes are preserved
- All errors are clearly reported

### Failure Handler

ScheduleLink includes a built-in Revit failure handler that:

1. **Captures warnings** — Deletes them silently and logs them (e.g., duplicate Mark values)
2. **Captures errors** — Attempts to resolve them for partial commit
3. **Reports everything** — All warnings and errors appear in the results dialog with element names and IDs

### Common Errors

| Error | Cause | Solution |
|-------|-------|----------|
| **Element not found** | Element deleted after export | Re-export the schedule |
| **Duplicate Sheet Number** | Two rows have the same Sheet Number in Excel | Fix the duplicate in Excel |
| **Failed to set value** | Invalid value for parameter type | Check data type (number vs. text) |
| **Commit error** | Revit rejected the transaction | Check Revit warnings |

### Revit Warnings vs. Errors

| Type | Behavior | Example |
|------|----------|---------|
| **Warning** | Change is applied, warning is logged | Duplicate Mark value |
| **Error** | Change is blocked, error is logged | Duplicate Sheet Number |

---

## 12. Log Files

For advanced troubleshooting, ScheduleLink creates log files at:

```
C:\ProgramData\IB-BIM\ScheduleLink\Logs\
```

| File | Description | Lifecycle |
|------|-------------|-----------|
| `ScheduleLink.log` | Main application log | Resets each Revit session |
| `ExportImport.log` | Detailed operation log | Resets each operation |

### Log Format

```
[14:32:15.123] [INFO] [Import] Pass 1: Setting 23 Sheet Numbers to temp values
[14:32:15.456] [INFO] [Import] Pass 2: Setting 23 Sheet Numbers to final values
[14:32:15.789] [INFO] [Import] ImportToRevit: Committed - Updated=21 Failed=2
```

Each entry includes timestamp, severity level, category, and message.

---

## 13. Tips and Best Practices

### Before Exporting
- Save your Revit file as a backup
- Ensure the schedule view shows all the parameters you need

### While Editing in Excel
- **Use Find & Replace** for bulk changes across many rows
- **Use Excel formulas** to generate values (copy-paste as values before importing)
- **Conditional formatting** can help identify duplicates (especially for Sheet Numbers)
- Don't forget to **save and close** the Excel file before importing

### After Importing
- Review the results dialog carefully
- Open the schedule in Revit to verify changes visually
- If something went wrong, **Ctrl+Z** immediately — all changes are reverted in one step

> 💡 **No backup needed.** Unlike other tools, ScheduleLink uses a single Revit transaction. If anything goes wrong, simply press **Ctrl+Z** to undo all changes instantly. Your project is always safe.

### Working with Sheet Lists
- Always check for duplicate Sheet Numbers before importing
- Use Excel's `COUNTIF` formula to detect duplicates:  
  `=COUNTIF(B:B, B2)` — values > 1 indicate duplicates

---

## 14. Uninstallation

### Via Control Panel
1. Go to **Control Panel** → **Programs and Features**
2. Find **ScheduleLink** and click **Uninstall**
3. Restart Revit

### Via Autodesk App Store
Use the Autodesk App Store desktop app to manage and remove installed add-ins.

---

<p align="center">
  <strong>© 2026 IB-BIM. All rights reserved.</strong><br>
  <a href="https://github.com/itzikb49">GitHub</a> · 
  <a href="https://apps.autodesk.com/">Autodesk App Store</a>
</p>
