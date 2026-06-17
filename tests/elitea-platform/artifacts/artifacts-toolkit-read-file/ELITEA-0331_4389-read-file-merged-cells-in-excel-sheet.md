---
id: ELITEA-0331
title: "[#4389] read_file — Merged Cells in Excel Sheet"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, issue:4389, read_file, edge-case, r-2.0.3, excel]
requirements: [4389]
---
# ELITEA-0331: [#4389] read_file — Merged Cells in Excel Sheet

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that `read_file` handles Excel sheets with merged cells without crashing. Output should be understandable and consistent — no row/column misalignment, no crashes, and merged cell values are returned without data loss.

## Preconditions

User is logged in to ELITEA.
Artifacts Toolkit is configured via Toolkit Test Settings.
`merged_cells.xlsx` is uploaded to an artifact bucket.
Sheet \"Report\" contains:
- Row 1: A1:C1 merged with the value \"Quarterly Report\" (header spanning 3 columns)
- Rows 2–5: regular unmerged data rows with known values
- Row 6: A6:B6 merged with value \"Subtotal\", C6 contains 999

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `read_file` with `sheet_name`: "Report". | Response is returned without crash or unhandled exception. Merged header "Quarterly Report" is present in the output (in some form — value, not blank). Regular data rows 2–5 are returned with correct values. Row 6 "Subtotal" value is present; C6=999 is present. No row or column misalignment that makes the data uninterpretable. |
| 2 | Call `read_file` with `sheet_name`: "Report", `start_row`: 1, `end_row`: 1 (merged header row only). | The merged header row is returned. "Quarterly Report" value is present. No crash. No empty output for a row that visibly contains data. |
| 3 | Call `read_file` with `sheet_name`: "Report", `start_row`: 6, `end_row`: 6 (partially merged data row). | Row 6 is returned. "Subtotal" and 999 are both present. No crash or data loss due to the merged cell spanning A6:B6. |

## Expected Final State

Row 6 is returned. "Subtotal" and 999 are both present. No crash or data loss due to the merged cell spanning A6:B6.

## Pass/Fail Criteria

PASS: No crash; merged values present in output; no column misalignment; data from regular rows unaffected.
FAIL: Crash or 500 error; merged cell value blank; data rows misaligned due to merge; tool unusable after merged-cell read.
