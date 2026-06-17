---
id: ELITEA-0327
title: "[#4389] read_file / get_file_metadata — Sheet Names with Special Characters and Unicode"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, issue:4389, read_file, unicode, r-2.0.3, excel]
requirements: [4389]
---
# ELITEA-0327: [#4389] read_file / get_file_metadata — Sheet Names with Special Characters and Unicode

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that `get_file_metadata` returns sheet names correctly when they contain spaces, non-Latin Unicode text (Russian, Armenian), and symbols. Verify that `read_file` with those exact names as `sheet_name` reads the correct sheet content.

## Preconditions

User is logged in to ELITEA.
Artifacts Toolkit is configured via Toolkit Test Settings.
`special_sheets.xlsx` is uploaded to an artifact bucket. It contains the following sheets:
- \"Sales Data\" (name with a space)
- \"русс\" (Cyrillic)
- \"հայ\" (Armenian)
- \"@#$%^&\" (symbols)
Each sheet has at least 3 rows of unique identifiable content.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `get_file_metadata` on `special_sheets.xlsx`. | Response includes all four sheet names exactly as stored: - "Sales Data" - "русс" - "հայ" - "@#$%^&" No name is mangled, percent-encoded, or truncated. |
| 2 | Call `read_file` with: - file path: `special_sheets.xlsx` - `sheet_name`: "Sales Data" (with space) | Content of the "Sales Data" sheet is returned correctly. No error about sheet not found. |
| 3 | Call `read_file` with `sheet_name`: "русс" (Cyrillic). | Content of the Cyrillic-named sheet is returned correctly. Unicode name is handled without encoding errors. |
| 4 | Call `read_file` with `sheet_name`: "հայ" (Armenian). | Content of the Armenian-named sheet is returned correctly. |
| 5 | Call `read_file` with `sheet_name`: "@#$%^&" (symbols). | Content of the symbol-named sheet is returned correctly. No parsing or escape errors. |

## Expected Final State

Content of the symbol-named sheet is returned correctly. No parsing or escape errors.

## Pass/Fail Criteria

PASS: All sheet names preserved exactly; all sheet_name reads return correct content.
FAIL: Any name mangled, truncated, or percent-encoded; any "sheet not found" error for a valid special-character name.
