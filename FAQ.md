---
layout: default
title: "ScheduleLink — FAQ"
---

[← Back to Home](index.md)

# ❓ IB-BIM ScheduleLink — Frequently Asked Questions

<p align="center">
  <img src="Images/IB-BIM_200X200.png" alt="IB-BIM Logo" width="100">
</p>

---

## Table of Contents

- [General](#general)
- [Export](#export)
- [Import](#import)
- [Sheet Numbers](#sheet-numbers)
- [Excel Editing](#excel-editing)
- [Errors and Troubleshooting](#errors-and-troubleshooting)
- [Performance](#performance)
- [Data and Privacy](#data-and-privacy)

---

## General

### What is ScheduleLink?

ScheduleLink is a Revit add-in that allows you to export any Revit schedule to Excel, edit values, and import them back. Changes are applied directly to the Revit elements — not just the schedule view.

### Which Revit versions are supported?

Revit 2023, 2024, 2025, and 2026.

### Does it work with all schedule types?

Yes. Any schedule in your Revit project is supported — Room Schedules, Sheet Lists, Door Schedules, Equipment Schedules, Material Takeoffs, and custom schedules.

### Where does the ScheduleLink button appear?

In the **Add-Ins** tab in the Revit ribbon.

---

## Export

### Can I export multiple schedules at once?

Currently, ScheduleLink exports one schedule at a time. Select a schedule from the list and click Export.

### Why are some columns colored pink or gray?

Pink or gray columns are **read-only**. These parameters cannot be modified via the Revit API (e.g., calculated values, system parameters). They are included for reference only.

### Does export include filtered elements?

Yes. ScheduleLink exports all elements in the schedule, including those hidden by schedule filters.

### What format is the export file?

Excel (.xlsx) with formatted headers, color-coded columns, auto-filter, and frozen header row.

---

## Import

### Can I undo the import?

Yes. All changes are made in a single Revit transaction. Press **Ctrl+Z** to undo everything at once.

### What happens if I change a read-only column?

Nothing. Changes to read-only columns are silently ignored. The results dialog shows the count of skipped read-only values.

### What happens if I delete a row in Excel?

The deleted row is not processed. The corresponding Revit element remains unchanged. No error is reported.

### What happens if I add a new row in Excel?

New rows are ignored. ScheduleLink only updates existing elements identified by their Element ID. It does not create new elements.

### Can I reorder rows in Excel?

Yes. ScheduleLink matches rows by Element ID, not by row position. You can sort or reorder rows freely.

### Can I reorder columns in Excel?

No. Column order must match the original export. Do not add, remove, or rearrange columns.

---

## Sheet Numbers

### Why do I get "Duplicate Sheet Number" errors?

Your Excel file contains two or more rows with the same Sheet Number. Since Revit requires unique Sheet Numbers, ScheduleLink detects the duplicates and restores the original Revit values.

**Solution:** Open Excel, find duplicates using `=COUNTIF(B:B, B2)`, fix them, and re-import.

### I'm renaming multiple sheets — will it work?

Yes. ScheduleLink uses a **two-pass algorithm**:

1. All Sheet Numbers are set to temporary values (clearing all originals)
2. All Sheet Numbers are set to their final values from Excel

This prevents "already in use" errors when swapping numbers between sheets.

### What if I accidentally create a duplicate Sheet Number?

ScheduleLink detects it before applying:
- The duplicate values are **not applied**
- Original Revit values are **restored**
- A clear error message tells you which rows and values are affected
- All other changes proceed normally

---

## Excel Editing

### What data types are supported?

| Type | Format |
|------|--------|
| Text | Any text |
| Number | `42` or `3.14` |
| Yes/No | `Yes`/`No`, `1`/`0`, `True`/`False`, `כן`/`לא` |
| Length | Numeric value (units auto-converted) |

### Can I use Excel formulas?

Yes, but **copy-paste as values** before importing. ScheduleLink reads cell values, not formulas.

### Can I save as CSV?

No. Always save as **.xlsx**. CSV and .xls formats are not supported.

### Does the file need to be closed before importing?

Yes. If Excel has the file open, the import may fail. Save and close the file first.

---

## Errors and Troubleshooting

### Import shows "Element not found"

The element was deleted from Revit after the Excel file was exported. Re-export the schedule to get a fresh file.

### Import shows "Failed to set" for a parameter

The value format doesn't match the parameter type. Check that numbers are plain numbers (no currency symbols or unit text), and Yes/No fields use the accepted values.

### The ScheduleLink button doesn't appear

- Close and reopen Revit
- Check Add-Ins tab → External Tools
- Reinstall the add-in
- Verify your Revit version is supported (2023–2026)

### Changes don't appear after import

- Check the results dialog — were changes listed as "Updated"?
- Refresh the schedule view (close and reopen it)
- Check if Revit warnings appeared

### The results dialog shows warnings

Warnings (like duplicate Mark values) are informational. The changes were applied successfully. Revit generated a warning, and ScheduleLink captured it for your information.

---

## Performance

### How fast is ScheduleLink?

| Schedule Size | Approximate Time |
|--------------|-----------------|
| 10–100 rows | < 1 second |
| 100–500 rows | 1–3 seconds |
| 500–1000 rows | 3–10 seconds |
| 1000+ rows | 10+ seconds |

### Is there a row limit?

No hard limit. ScheduleLink can handle schedules with thousands of rows. Very large schedules take longer but work correctly.

---

## Data and Privacy

### Does ScheduleLink send data online?

ScheduleLink communicates only with:
- **Autodesk servers** — License verification (Entitlement API)
- **GitHub** — Update checking (version.json only)

Your Revit project data **never** leaves your computer.

### Can ScheduleLink corrupt my Revit file?

No. All changes go through the standard Revit API transaction mechanism. If anything goes wrong, Revit's built-in safety features prevent data corruption. Additionally, you can always **Ctrl+Z** to undo.

---

<p align="center">
  <strong>© 2026 IB-BIM. All rights reserved.</strong><br>
  <a href="https://github.com/itzikb49">GitHub</a> · 
  <a href="https://apps.autodesk.com/">Autodesk App Store</a>
</p>
