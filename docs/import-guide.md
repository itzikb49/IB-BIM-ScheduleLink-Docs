# Import Guide

## How to Import Changes from Excel

### Step 1: Prepare Your Excel File

Before importing, make sure:

- ✅ The **Element ID** column (column A) is intact and unmodified
- ✅ You only changed values in **white** (editable) columns
- ✅ The file is saved and closed in Excel
- ✅ No duplicate values in unique fields (like Sheet Number)

### Step 2: Click Import

In the ScheduleLink dialog, click the **Import** button. A file dialog opens — select your modified Excel file.

### Step 3: Review Results

After import completes, a results dialog shows:

| Field | Description |
|-------|-------------|
| **Rows** | Total number of data rows in the Excel file |
| **Updated** | Number of parameter values successfully changed |
| **Unchanged** | Values that matched Revit (no change needed) |
| **Read-only (skipped)** | Edits in read-only columns (ignored) |
| **Not found** | Elements with invalid or missing Element IDs |
| **Failed** | Values that could not be applied (with error details) |

### Step 4: Verify in Revit

After import:
- Open the schedule view in Revit to verify changes
- Use **Ctrl+Z** to undo all changes if something went wrong (single undo operation)

---

## How Import Works

### Standard Parameters

ScheduleLink reads each row from Excel, finds the corresponding Revit element by Element ID, and updates each editable parameter to the new value.

### Sheet Numbers (Two-Pass Algorithm)

Sheet Numbers are unique in Revit — no two sheets can have the same number. To prevent conflicts when renaming multiple sheets, ScheduleLink uses a special approach:

1. **Pass 1** — All Sheet Numbers are temporarily set to unique placeholder values
2. **Pass 2** — All Sheet Numbers are set to their final values from Excel

This prevents "already in use" errors when swapping sheet numbers between sheets.

### Duplicate Detection

Before applying Sheet Numbers, ScheduleLink checks for duplicates in the Excel file. If found:

- The duplicate values are **not applied**
- The original Revit values are **restored**
- A clear error message is shown in the results dialog

### Error Handling

If a parameter fails to update:

- The error is logged and reported in the results dialog
- Other parameters continue to be processed normally
- The transaction commits with all successful changes

Revit warnings (like duplicate Mark values) are captured and reported but do not prevent the import from completing.

---

## Import Results — Error Messages

| Error | Cause | Solution |
|-------|-------|----------|
| **Element not found** | Element was deleted from Revit after export | Re-export the schedule |
| **Duplicate Sheet Number** | Two rows have the same Sheet Number | Fix the duplicate in Excel |
| **Failed to set value** | Invalid value for the parameter type | Check the value format (number, text, etc.) |
| **Commit error** | Revit rejected the transaction | Check Revit warnings for details |

---

## Tips for Import

- **Always keep a backup** — Export a fresh copy before making bulk changes
- **Close Excel first** — The file must not be locked by Excel during import
- **Check data types** — Numbers should be numbers, not text with spaces
- **Yes/No parameters** — Use "Yes"/"No", "1"/"0", or "True"/"False"
- **Small batches** — For large changes, consider importing in smaller groups
- **Ctrl+Z** — All changes are in a single transaction and can be undone with one Ctrl+Z
