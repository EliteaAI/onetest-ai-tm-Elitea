---
id: ELITEA-4429
title: "Verify Excel export functionality downloads correct data"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, export, excel]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User is on skill run analytics page with data
- Export button is visible in header (typically top-right)
- Analytics data has loaded successfully

## Test Data

| Field | Value |
|-------|-------|
| Export Format | Excel (.xlsx) |
| File Naming | Should include skill name and run timestamp |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On analytics page, locate export/download button | Button visible in top-right corner |
| 2 | Click export button | Export options menu opens (if multiple formats) |
| 3 | Select "Export to Excel" option | Download initiates |
| 4 | Wait for download to complete | Excel file downloads successfully |
| 5 | Locate downloaded file | File appears in Downloads folder |
| 6 | Verify file name includes skill name and run timestamp | File naming is descriptive |
| 7 | Open downloaded Excel file | File opens in Excel/spreadsheet application |
| 8 | Verify Excel contains sheets for: Costs, Tokens, Health | Sheets present (Tools if applicable) |
| 9 | Verify Costs sheet contains all cost table data | All tables from Costs tab included |
| 10 | Verify Tokens sheet contains all token table data | All tables from Tokens tab included |
| 11 | Verify Health sheet contains event and error data | All tables from Health tab included |
| 12 | (If applicable) Verify Tools sheet contains tool data | Tools tab data included if visible |
| 13 | Compare Excel data with UI displayed data | Data matches exactly |
| 14 | Verify formatting is clean and readable | Proper column headers, no truncation |

## Expected Final State

Excel export:
- Export button visible and clickable
- Excel file downloads successfully (.xlsx format)
- File name includes skill name and run timestamp
- Excel contains sheets: Costs, Tokens, Health (and Tools if applicable)
- All table data from each tab included
- Data in Excel matches UI displayed data
- Formatting clean and readable

## Pass/Fail Criteria

**Pass:**
- Export button works
- Excel file downloads (.xlsx)
- File naming descriptive
- All required sheets present
- All data from UI included
- Data matches UI exactly
- Formatting clean and readable

**Fail:**
- Export button missing or broken
- Download fails
- File format incorrect
- Missing sheets or data
- Data doesn't match UI
- Formatting poor or unreadable
- File corrupted or won't open
