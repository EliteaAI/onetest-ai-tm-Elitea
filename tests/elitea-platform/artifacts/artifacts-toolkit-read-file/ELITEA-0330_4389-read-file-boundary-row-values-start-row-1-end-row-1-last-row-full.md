---
id: ELITEA-0330
title: "[#4389] read_file — Boundary Row Values (start_row=1, end_row=1, last row, full valid range)"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, issue:4389, read_file, boundary, r-2.0.3, excel]
requirements: [4389]
---
# ELITEA-0330: [#4389] read_file — Boundary Row Values (start_row=1, end_row=1, last row, full valid range)

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify exact boundary row reads: first row only, a single middle row, the last row only, and the complete valid range. Complements the high-out-of-bounds error tests with correct boundary behavior checks.

## Preconditions

User is logged in to ELITEA.
Artifacts Toolkit is configured via Toolkit Test Settings.
`multi_sheet.xlsx` is uploaded to an artifact bucket.
The \"Data\" sheet has exactly 30 rows with known content:
- Row 1: header row (\"ID\", \"Name\", \"Value\")
- Row 30: last data row with known values (e.g., ID=30, Name=\"Last\", Value=999)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `read_file` with `sheet_name`: "Data", `start_row`: 1, `end_row`: 1. | Exactly 1 row is returned — the first row (header). No other rows present. |
| 2 | Call `read_file` with `sheet_name`: "Data", `start_row`: 30, `end_row`: 30. | Exactly 1 row is returned — the last row (ID=30, Name="Last", Value=999). No other rows present. |
| 3 | Call `read_file` with `sheet_name`: "Data", `start_row`: 1, `end_row`: 30. | All 30 rows are returned. Row count = 30. First and last row content matches expected values. |
| 4 | Call `read_file` with `sheet_name`: "Data", `start_row`: 15, `end_row`: 15 (single middle row). | Exactly 1 row is returned — row 15. Content matches the known value at row 15. No surrounding rows included. |

## Expected Final State

Exactly 1 row is returned — row 15. Content matches the known value at row 15. No surrounding rows included.

## Pass/Fail Criteria

PASS: Row count and content exact for all four boundary scenarios; no off-by-one errors.
FAIL: Extra rows returned; boundary row missing; wrong row count; content mismatch at row 1 or row 30.
