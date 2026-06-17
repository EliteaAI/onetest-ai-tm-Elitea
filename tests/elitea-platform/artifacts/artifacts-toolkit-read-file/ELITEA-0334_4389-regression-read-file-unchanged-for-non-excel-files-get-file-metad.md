---
id: ELITEA-0334
title: "[#4389] Regression — read_file Unchanged for Non-Excel Files; get_file_metadata Rename from get_file_type"
priority: high
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [get_file_metadata, feat:artifacts, regression, issue:4389, read_file, r-2.0.3]
requirements: [4389]
---
# ELITEA-0334: [#4389] Regression — read_file Unchanged for Non-Excel Files; get_file_metadata Rename from get_file_type

**Module:** Artifacts Toolkit Read File · **Priority:** High · **Type:** Functional

**Objective:** Regression verification: (1) `read_file` on .xlsx without new params behaves identically to before; (2) `read_file` on non-Excel files (.pdf, .docx, .txt, .csv) is unaffected; (3) `get_file_metadata` is the correct tool name (renamed from `get_file_type`) and is accessible in the UI.

## Preconditions

User is logged in to ELITEA.
Artifacts Toolkit is configured via Toolkit Test Settings.
Test files uploaded to a bucket: sample.xlsx, sample.pdf, sample.docx, sample.txt, data.csv.
PR for issue #4389 has been deployed to the environment.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Toolkit Test Settings → Artifacts Toolkit. Check the tool list available. | `get_file_metadata` is present in the tool list. `get_file_type` is NOT present (it has been renamed/removed). No broken or duplicate entries. |
| 2 | Call `read_file` on `sample.xlsx` without any new Excel parameters (no sheet_name, no row_by_row, no start_row/end_row). | Response is identical to pre-enhancement behavior — full file content returned (or first sheet content, per existing default). No new error or changed output format. |
| 3 | Call `read_file` on `sample.pdf` without any new parameters. | PDF content returned correctly. No error introduced by the Excel enhancement. |
| 4 | Call `read_file` on `sample.docx` without any new parameters. | DOCX text content returned correctly. No regression. |
| 5 | Call `read_file` on `sample.txt` and `data.csv` without new parameters. | Both files return their content correctly. No errors or changed behavior. |
| 6 | Call `get_file_metadata` on `sample.pdf` (non-Excel file). | Response does not include a `sheet_names` field (or it is null/absent — as Excel-specific metadata is not applicable). No error or crash for a non-Excel file type. |

## Expected Final State

Response does not include a `sheet_names` field (or it is null/absent — as Excel-specific metadata is not applicable). No error or crash for a non-Excel file type.

## Pass/Fail Criteria

PASS: get_file_type absent, get_file_metadata present; all non-Excel reads unaffected; xlsx default call unchanged; non-Excel metadata call graceful.
FAIL: get_file_type still present; any non-Excel read returns an error; xlsx default call changes behavior.
