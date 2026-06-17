---
id: ELITEA-0326
title: "[EliteaAI/elitea_issues#4389] get_file_metadata + read_file — Empty Sheet and Header-Only Sheet Handling"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, issue:4389, read_file, edge-case, r-2.0.3, excel]
requirements: [4389]
---
# ELITEA-0326: [EliteaAI/elitea_issues#4389] get_file_metadata + read_file — Empty Sheet and Header-Only Sheet Handling

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that `get_file_metadata` still lists empty and header-only sheets, and that `read_file` returns a sensible result for those sheets without crashing or returning misleading row counts.

## Preconditions

User is logged in to ELITEA.
Artifacts Toolkit is configured via Toolkit Test Settings.
`edge_sheets.xlsx` is uploaded to an artifact bucket with the following sheets:
- \"Empty\" — completely blank (no data, no headers)
- \"HeaderOnly\" — one row of column headers, no data rows
- \"Normal\" — regular sheet with headers + 10 data rows (reference sheet)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `get_file_metadata` on `edge_sheets.xlsx`. | Response lists all three sheets: "Empty", "HeaderOnly", "Normal". No crash. Empty and header-only sheets are included in the sheet list. |
| 2 | Call `read_file` with `sheet_name`: "Empty". | Response returns an empty result or a clear message indicating no data is present (e.g., empty array, "no rows"). No crash, no misleading row count, no fabricated data. |
| 3 | Call `read_file` with `sheet_name`: "HeaderOnly". | Response returns the header row only. No data rows are invented or duplicated. Row count is 1 (or 0 data rows with headers shown). |
| 4 | Call `read_file` with `sheet_name`: "Empty", `start_row`: 1, `end_row`: 5. | Returns empty result or a descriptive message. Does not crash or return rows that do not exist. |

## Expected Final State

Returns empty result or a descriptive message. Does not crash or return rows that do not exist.

## Pass/Fail Criteria

PASS: Empty sheet listed in metadata; read returns empty/clean result; no crash; no fabricated rows.
FAIL: Empty sheet missing from metadata; crash on read; non-existent rows returned; misleading row count.
