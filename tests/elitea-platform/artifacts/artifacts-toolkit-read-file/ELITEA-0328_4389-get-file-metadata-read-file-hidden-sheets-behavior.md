---
id: ELITEA-0328
title: "[#4389] get_file_metadata + read_file — Hidden Sheets Behavior"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, issue:4389, read_file, edge-case, r-2.0.3, excel]
requirements: [4389]
---
# ELITEA-0328: [#4389] get_file_metadata + read_file — Hidden Sheets Behavior

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the behavior of `get_file_metadata` and `read_file` for Excel workbooks containing hidden sheets. The expected behavior must be explicitly defined and consistent: hidden sheets are either always included or always excluded from metadata and reads.

## Preconditions

User is logged in to ELITEA.
Artifacts Toolkit is configured via Toolkit Test Settings.
`hidden_sheets.xlsx` is uploaded to an artifact bucket with:
- \"Visible\" — a normal visible sheet with 5 rows of data
- \"HiddenSheet\" — a hidden sheet (hidden via Format → Hide Sheet in Excel) with 3 rows of data
- \"AlsoVisible\" — another visible sheet with 5 rows

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `get_file_metadata` on `hidden_sheets.xlsx`. | Observe and record whether `sheet_names` includes "HiddenSheet" or not. Either outcome is acceptable, but the result must be consistent with the `read_file` behavior below. Document the actual behavior as the expected behavior for this environment. |
| 2 | Call `read_file` with `sheet_name`: "Visible". | Content of the "Visible" sheet is returned correctly. No error. |
| 3 | Call `read_file` with `sheet_name`: "HiddenSheet". | If metadata included "HiddenSheet" in step 1: content is returned correctly. If metadata excluded "HiddenSheet" in step 1: a clear "sheet not found" error is returned — behavior is consistent with metadata. |
| 4 | Verify consistency between metadata and read behavior. | The set of sheets accessible via `read_file` exactly matches the set returned by `get_file_metadata`. No sheet is accessible via read but absent from metadata, and vice versa. |

## Expected Final State

The set of sheets accessible via `read_file` exactly matches the set returned by `get_file_metadata`. No sheet is accessible via read but absent from metadata, and vice versa.

## Pass/Fail Criteria

PASS: Metadata and read_file are consistent for hidden sheets; no contradiction between the two tools.
FAIL: Hidden sheet appears in metadata but returns "not found" on read; or is readable but not listed in metadata.
