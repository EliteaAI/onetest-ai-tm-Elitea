---
id: ELITEA-2813
title: "Regression - read_file_from_sharing_link Oversized Excel Workbook Guidance"
priority: critical
type: regression
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:toolkits, issue:6051, excel, content-too-large, read_file_from_sharing_link]
requirements: [EliteaAI/elitea_issues#6051]
---
# ELITEA-2813: Regression - read_file_from_sharing_link Oversized Excel Workbook Guidance

**Module:** Sharepoint · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that the Excel pre-parse-estimate size guard on `read_file_from_sharing_link` produces "content too large" guidance instead of crashing when reading a very large multi-sheet `.xlsx` workbook.

Scoped only to the pre-parse size/row estimate guard. Does **not** include a `sheet_name`-parameter step — already covered by the Artifacts-toolkit test `ELITEA-0335` and intentionally not duplicated here.

## Preconditions

- SharePoint Delegated credential is connected and authenticated
- A sharing link to a very large `.xlsx` file with multiple sheets is available

## Test Data

| Field | Value |
|-------|-------|
| File | Large multi-sheet `.xlsx` workbook, sized to trigger the pre-parse row/size estimate guard |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `read_file_from_sharing_link` on the large `.xlsx` via the sharing link | "Content too large" guidance is returned; no crash or unhandled exception |

## Expected Final State

The oversized Excel workbook returns well-formed "content too large" guidance, with no crash.

## Pass/Fail Criteria

**Pass:**
- Guidance is returned correctly

**Fail:**
- Crash or unhandled exception
- Content is returned in full despite exceeding the size/row estimate guard
