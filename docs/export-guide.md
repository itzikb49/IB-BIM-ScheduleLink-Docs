# Export Guide

## How to Export a Schedule to Excel

### Step 1: Select a Schedule

In the ScheduleLink dialog, click on the schedule you want to export. Use the **search box** to filter by name if you have many schedules.

The right panel shows a preview of all parameters with their editability status.

### Step 2: Click Export

Click the **Export** button at the bottom of the dialog. A **Save File** dialog opens.

Choose a location and filename for your Excel file. The default filename is the schedule name.

### Step 3: Wait for Completion

A progress bar shows the export progress. For large schedules (1000+ rows), this may take a few seconds.

When complete, a confirmation message appears with the number of rows and columns exported.

---

## Excel File Structure

The exported Excel file contains two sheets:

### Data Sheet (Schedule Name)

This is the main sheet with your schedule data:

| Column | Description |
|--------|-------------|
| **A — Element ID** | Unique Revit element identifier (hidden by default). **Do not modify.** |
| **B, C, D...** | Schedule parameters in the same order as in Revit |

### Instructions Sheet

Contains metadata about the export:

- Schedule name and ID
- Export date and time
- Revit version
- Column descriptions and editability status

---

## Column Color Coding in Excel

| Background Color | Meaning |
|-----------------|---------|
| **White** | Editable — you can modify these values |
| **Pink / Gray** | Read-only — changes will be ignored during import |
| **Green header** | Standard parameter column |

---

## Tips for Export

- **Large schedules** — Export may take longer for schedules with thousands of rows. The progress bar shows real-time status.
- **Filtered schedules** — ScheduleLink exports **all elements** in the schedule, including those hidden by filters.
- **Grouped schedules** — Elements are exported in their natural order, not by groups.
- **Element ID column** — This column is essential for import. Never delete or modify it.

---

## After Export

1. Open the Excel file
2. Review the column colors to understand which columns are editable
3. Make your changes in the **white** columns only
4. Save the file
5. Use [Import](import-guide.md) to apply changes back to Revit
