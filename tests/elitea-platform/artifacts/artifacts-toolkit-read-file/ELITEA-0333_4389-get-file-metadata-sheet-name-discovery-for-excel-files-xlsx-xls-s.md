---
id: ELITEA-0333
title: "[#4389] get_file_metadata — Sheet Name Discovery for Excel Files (.xlsx, .xls, single/multi/large sheet)"
priority: high
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [get_file_metadata, feat:artifacts, issue:4389, r-2.0.3, excel]
requirements: [4389]
---
# ELITEA-0333: [#4389] get_file_metadata — Sheet Name Discovery for Excel Files (.xlsx, .xls, single/multi/large sheet)

**Module:** Artifacts Toolkit Read File · **Priority:** High · **Type:** Functional

**Objective:** Verify that `get_file_metadata` correctly returns sheet names for Excel files without reading cell content. Covers .xlsx (multi-sheet), .xls (legacy format), single-sheet file, and large file with 10+ sheets.

## Preconditions

User is logged in to ELITEA.
Artifacts Toolkit is configured and accessible via Toolkit Test Settings.
Test files are uploaded to an artifact bucket:
- multi_sheet.xlsx — 3+ sheets named e.g. "Summary", "Data", "Config"
- legacy.xls — 2+ sheets
- single_sheet.xlsx — exactly 1 sheet
- large_multi.xlsx — 10+ sheets

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Toolkit Test Settings for the Artifacts Toolkit. Select the `get_file_metadata` tool. Call it with the path to `multi_sheet.xlsx`. | Response is returned without error. Response includes a `sheet_names` field (or equivalent) listing all sheet names (e.g. ["Summary", "Data", "Config"]). No cell content is included in the response. |
| 2 | Call `get_file_metadata` with the path to `legacy.xls`. | Response includes the correct list of sheet names from the .xls file. No error or unsupported format message. |
| 3 | Call `get_file_metadata` with the path to `single_sheet.xlsx`. | Response includes `sheet_names` with exactly one entry — the single sheet name. No empty list or error returned. |
| 4 | Call `get_file_metadata` with the path to `large_multi.xlsx` (10+ sheets). | All 10+ sheet names are returned in the response. No truncation, timeout, or crash occurs. |

## Expected Final State

All 10+ sheet names are returned in the response. No truncation, timeout, or crash occurs.

## Pass/Fail Criteria

PASS: `sheet_names` field present and accurate for all file variants; no cell data returned; no errors.
FAIL: Sheet names missing, truncated, or cell content included; any crash or 500 error.
