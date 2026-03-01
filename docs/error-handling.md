# Error Handling

## Overview

ScheduleLink is designed to handle errors gracefully. A single error does not cancel the entire operation — successful changes are preserved while errors are clearly reported.

---

## Results Dialog

After every import, a results dialog shows a complete summary:

```
Rows: 23
Updated: 21
Unchanged: 115
Read-only (skipped): 0
Not found: 0
Failed: 2

Errors:
  Row 10: Excel value 'BNAV-SA-F02-P-01' is duplicate → kept Revit value 'BNAV-SA-F02-P-01'
  Row 24: Excel value 'BNAV-SA-F02-P-01' is duplicate → kept Revit value 'BNAV-SA-F08-P-03'
```

---

## Error Types

### Element Not Found

**Message:** `Row X: Element 12345 not found`

**Cause:** The element was deleted from the Revit project after the Excel file was exported.

**Solution:** Re-export the schedule to get a fresh file with current Element IDs.

---

### Duplicate Sheet Number

**Message:** `Row X: Excel value 'ABC-123' is duplicate → kept Revit value 'ABC-456'`

**Cause:** Two or more rows in the Excel file have the same Sheet Number value. Since Revit requires unique Sheet Numbers, the duplicate values cannot be applied.

**What happens:**
- The original Revit value is restored for all rows with the duplicate value
- All other (non-duplicate) changes are applied normally
- The error is reported in the results dialog

**Solution:** Open the Excel file, find the duplicate Sheet Numbers, and correct them. Then re-import.

---

### Failed to Set Value

**Message:** `Row X: Failed to set 'Parameter Name' = 'value'`

**Cause:** The value could not be applied to the parameter. Common reasons:
- Text value in a numeric field
- Value out of range
- Invalid format

**Solution:** Check the value format matches the parameter type (see [Excel Format](excel-format.md#supported-data-types)).

---

### Revit Warnings

**Message:** `[Warning] Description text | Element Name (id 12345)`

**Cause:** Revit generated a warning during the import (e.g., duplicate Mark values). The operation was completed successfully despite the warning.

**What happens:**
- The change was applied
- The warning is logged for your information
- No action is required unless the warning indicates a real problem

---

### Revit Errors

**Message:** `[Error] Description text | Element Name (id 12345)`

**Cause:** Revit blocked a specific change. The error is captured and reported, and all other changes proceed normally.

**Solution:** Review the error description. You may need to fix the value manually in Revit.

---

### Commit Error

**Message:** `Commit error: Description`

**Cause:** The entire transaction failed to commit. This is rare and usually indicates a serious Revit constraint violation.

**What happens:**
- All changes in this import are rolled back
- No data is modified

**Solution:** Check the error message, fix the underlying issue, and try again.

---

## Failure Handler

ScheduleLink includes a built-in failure handler that:

1. **Captures Revit warnings** — Deletes them silently and logs them
2. **Captures Revit errors** — Attempts to resolve them to allow partial commit
3. **Reports everything** — All warnings and errors appear in the results dialog

This means:
- A warning on one element does not affect other elements
- An error on one element is reported but does not cancel the import
- The results dialog gives you full visibility into what happened

---

## Undo

All import changes are wrapped in a **single Revit transaction**. If the results are not what you expected:

- Press **Ctrl+Z** in Revit to undo all changes at once
- The project returns to its state before the import

> **Note:** Undo works only before saving the Revit file. After saving, changes are permanent.

---

## Log Files

For advanced troubleshooting, ScheduleLink creates log files at:

```
C:\ProgramData\IB-BIM\ScheduleLink\Logs\
```

| File | Description |
|------|-------------|
| `ScheduleLink.log` | Main application log (one per Revit session) |
| `ExportImport.log` | Detailed import/export log (one per operation) |

These files contain detailed information about each operation and can help diagnose issues.
