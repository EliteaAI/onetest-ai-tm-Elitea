---
id: ELITEA-0325
title: "[EliteaAI/elitea_issues#4389] read_file — Very Wide Sheet (Large Column Count)"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, issue:4389, read_file, edge-case, r-2.0.3, excel]
requirements: [4389]
---
# ELITEA-0325: [EliteaAI/elitea_issues#4389] read_file — Very Wide Sheet (Large Column Count)

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that `read_file` correctly handles a sheet with a very large number of columns (300+). Output must not be silently truncated, and any metadata column count must match what is actually readable.

## Preconditions

User is logged in to ELITEA.
Artifacts Toolkit is configured via Toolkit Test Settings.
`wide_sheet.xlsx` is uploaded to an artifact bucket:
- Contains a sheet named \"Wide\" with 359 columns and 5 rows of data.
- Columns span A to NW (or equivalent). Column headers are labeled Col_1 through Col_359.
- Known values exist in columns 1, 180, and 359 for row 1 (e.g., \"FIRST\", \"MIDDLE\", \"LAST\").

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `get_file_metadata` on `wide_sheet.xlsx`. | Sheet "Wide" is listed. If column metadata is included (e.g., `max_column`), the value is 359 or matches the actual column count. |
| 2 | Call `read_file` with `sheet_name`: "Wide". | Response includes data from all 359 columns. Column 1, column 180, and column 359 values ("FIRST", "MIDDLE", "LAST") are all present in the output. No silent truncation at a mid-column boundary (e.g., not cut off at column 256 or 100). |
| 3 | Call `read_file` with `sheet_name`: "Wide", `start_row`: 1, `end_row`: 2. | Only rows 1–2 are returned. All 359 columns are still present across both rows. No truncation. |

## Expected Final State

Only rows 1–2 are returned. All 359 columns are still present across both rows. No truncation.

## Pass/Fail Criteria

PASS: All columns present in output; known boundary column values (FIRST, MIDDLE, LAST) visible; no truncation.
FAIL: Output cut off before column 359; known values missing; metadata column count mismatches actual output.
