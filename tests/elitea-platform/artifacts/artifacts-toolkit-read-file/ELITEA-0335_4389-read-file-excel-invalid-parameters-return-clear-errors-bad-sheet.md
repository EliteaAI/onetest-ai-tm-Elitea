---
id: ELITEA-0335
title: "[#4389] read_file Excel — Invalid Parameters Return Clear Errors (bad sheet name, invalid row range, out-of-bounds)"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, error-handling, issue:4389, read_file, r-2.0.3, excel]
requirements: [4389]
---
# ELITEA-0335: [#4389] read_file Excel — Invalid Parameters Return Clear Errors (bad sheet name, invalid row range, out-of-bounds)

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify error handling for the new Excel parameters in `read_file`: non-existent sheet name, `start_row` greater than `end_row`, and `start_row` beyond the file's actual row count. Each case must return a clear, actionable message rather than crashing or returning empty output silently.

## Preconditions

User is logged in to ELITEA.
Artifacts Toolkit is configured via Toolkit Test Settings.
`multi_sheet.xlsx` is uploaded — known to have 30 rows in "Data" sheet.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `read_file` with: - file path: `multi_sheet.xlsx` - `sheet_name`: "NonExistentSheet" | A clear, actionable error message is returned (e.g., "Sheet 'NonExistentSheet' not found"). No crash, no silent empty output, no 500 server error. The tool remains usable for subsequent calls. |
| 2 | Call `read_file` with: - file path: `multi_sheet.xlsx` - `sheet_name`: "Data" - `start_row`: 50 - `end_row`: 10 (start > end) | A clear validation error is returned (e.g., "start_row cannot be greater than end_row"). No crash or empty result returned silently. |
| 3 | Call `read_file` with: - file path: `multi_sheet.xlsx` - `sheet_name`: "Data" - `start_row`: 500 (beyond the 30 rows in the file) | Returns an empty result with a descriptive message (e.g., "start_row exceeds file row count"), OR returns a clear out-of-bounds error. Does NOT crash or return fabricated data. |

## Expected Final State

Returns an empty result with a descriptive message (e.g., "start_row exceeds file row count"), OR returns a clear out-of-bounds error. Does NOT crash or return fabricated data.

## Pass/Fail Criteria

PASS: Each invalid scenario returns a descriptive error; tool remains usable; no crash or 500.
FAIL: Silent empty output without explanation; crash or unhandled exception; fabricated data returned.
