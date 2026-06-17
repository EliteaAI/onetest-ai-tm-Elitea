---
id: ELITEA-0336
title: "[#4389] read_file — Row Range and Sheet Selection for Excel Files (start_row, end_row, sheet_name)"
priority: high
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, row_by_row, issue:4389, read_file, r-2.0.3, excel]
requirements: [4389]
---
# ELITEA-0336: [#4389] read_file — Row Range and Sheet Selection for Excel Files (start_row, end_row, sheet_name)

**Module:** Artifacts Toolkit Read File · **Priority:** High · **Type:** Functional

**Objective:** Verify the new Excel-specific parameters of `read_file`: reading a specific sheet by name, and reading a row range with `start_row`/`end_row`. Both capabilities introduced by issue #4389.

## Preconditions

User is logged in to ELITEA.
Artifacts Toolkit is configured via Toolkit Test Settings.
`multi_sheet.xlsx` is uploaded to an artifact bucket — has at least 3 sheets, the "Data" sheet has 50+ rows of known content.
Test data: exact values in rows 10–20 of "Data" sheet are known in advance for verification.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Toolkit Test Settings for Artifacts Toolkit. Select `read_file`. Call `read_file` with: - file path: `multi_sheet.xlsx` - `sheet_name`: "Data" | Only the "Data" sheet content is returned. Content from other sheets ("Summary", "Config") is absent. No error. |
| 2 | Call `read_file` with: - file path: `multi_sheet.xlsx` - `sheet_name`: "Data" - `start_row`: 10 - `end_row`: 20 | Response contains exactly rows 10–20 of the "Data" sheet. Rows 1–9 and rows 21+ are not present in the output. Row content matches the known test data. |
| 3 | Call `read_file` with all params combined: - `sheet_name`: "Data" - `start_row`: 5 - `end_row`: 15 | Only rows 5–15 of the "Data" sheet are returned. Exact row count = 11 rows. Content matches test data. |

## Expected Final State

Only rows 5–15 of the "Data" sheet are returned. Exact row count = 11 rows. Content matches test data.

## Pass/Fail Criteria

PASS: Correct sheet returned; correct row range returned; combined params work.
FAIL: Wrong sheet or extra sheets returned; rows outside range included; any crash.
