# Frequently Asked Questions

## General

### What is ScheduleLink?

ScheduleLink is a Revit add-in that allows you to export any Revit schedule to Excel, edit the values, and import them back into Revit. It directly updates the element parameters — not just the schedule view.

### Which Revit versions are supported?

Revit 2023, 2024, 2025, and 2026.

### Does ScheduleLink work with all schedule types?

Yes. Any schedule that appears in your Revit project is supported, including Room Schedules, Sheet Lists, Door Schedules, Equipment Schedules, Material Takeoffs, and custom schedules.

---

## Export

### Can I export multiple schedules at once?

Currently, ScheduleLink exports one schedule at a time. Select the schedule from the list and click Export.

### Why are some columns colored pink/gray?

Pink or gray columns are **read-only**. These parameters cannot be modified via the API (e.g., calculated values, system parameters). They are included in the export for reference.

### Does export include filtered elements?

Yes. ScheduleLink exports all elements in the schedule, including those hidden by schedule filters.

---

## Import

### Can I undo the import?

Yes. All changes are made in a single Revit transaction. Press **Ctrl+Z** to undo everything at once.

### What happens if I change a read-only column?

Nothing. Changes to read-only columns are silently ignored during import. The results dialog shows the count of skipped read-only values.

### What happens if I delete a row in Excel?

The deleted row is simply not processed during import. The corresponding Revit element remains unchanged. No error is reported.

### What happens if I add a new row in Excel?

New rows are ignored. ScheduleLink only updates existing elements identified by their Element ID. It does not create new elements.

### Can I reorder rows in Excel?

Yes. ScheduleLink matches rows by Element ID, not by row position. You can sort or reorder rows freely.

### Can I reorder columns in Excel?

No. Column order must match the original export. Do not add, remove, or rearrange columns.

---

## Sheet Numbers

### Why do I get "Duplicate Sheet Number" errors?

Revit requires every sheet to have a unique Sheet Number. If your Excel file contains two or more rows with the same Sheet Number, ScheduleLink cannot apply those values and restores the original Revit values.

**Solution:** Open Excel, find the duplicate Sheet Numbers (use Excel's conditional formatting or COUNTIF to highlight duplicates), fix them, and re-import.

### I'm renaming multiple sheets — will it work?

Yes. ScheduleLink uses a two-pass algorithm specifically for Sheet Numbers:

1. First, all Sheet Numbers are set to temporary values (to free up all names)
2. Then, all Sheet Numbers are set to their final values from Excel

This prevents "already in use" errors when swapping names between sheets.

---

## Troubleshooting

### Import shows "Element not found"

The element was deleted from Revit after the Excel file was exported. Re-export the schedule to get a fresh file.

### Import shows "Failed to set" for a parameter

The value format doesn't match the parameter type. Check:
- Numbers should be plain numbers (no currency symbols, no units text)
- Yes/No fields accept: "Yes"/"No", "1"/"0", "True"/"False", "כן"/"לא"
- Text fields accept any value

### The Excel file won't open

Make sure:
- The file was saved as .xlsx (not .csv or .xls)
- The file is not corrupted
- You have Microsoft Excel or a compatible viewer installed

### ScheduleLink button doesn't appear in Revit

Try:
1. Close and reopen Revit
2. Check Add-Ins tab → External Tools
3. Reinstall the add-in
4. Check that your Revit version is supported (2023-2026)

### Changes don't appear after import

- Make sure you're looking at the correct schedule view
- Check the results dialog — were changes reported as "Updated"?
- Try refreshing the schedule view (close and reopen it)
- Check if Revit warnings appeared that might have prevented changes

---

## Performance

### How fast is the export/import?

Export and import speed depends on the schedule size:

| Rows | Approximate Time |
|------|-----------------|
| 10-100 | Instant (< 1 second) |
| 100-500 | 1-3 seconds |
| 500-1000 | 3-10 seconds |
| 1000+ | 10+ seconds |

A progress bar is shown during both export and import operations.

### Is there a row limit?

There is no hard limit. ScheduleLink can handle schedules with thousands of rows. Very large schedules (10,000+ rows) may take longer but will work correctly.

---

## Data Safety

### Can ScheduleLink corrupt my Revit file?

No. All changes go through the standard Revit API transaction mechanism. If anything goes wrong, Revit's built-in safety features prevent data corruption.

### Should I back up before importing?

It's always good practice to save your Revit file before any bulk operation. However, since import can be undone with Ctrl+Z, the risk is minimal.

### Does ScheduleLink send data online?

ScheduleLink only communicates with:
- **Autodesk servers** — For license verification (Entitlement API)
- **GitHub** — For update checking (version.json only, no project data)

Your Revit project data never leaves your computer.
