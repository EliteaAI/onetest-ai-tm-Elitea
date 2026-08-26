---
id: ELITEA-2781
title: "Oversized Excel Workbook via read_file_from_sharing_link Returns Guidance on Both Primary and 403-Fallback Paths"
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:toolkits, issue:6051, excel, content-too-large, cross-tenant-fallback, 403-fallback]
requirements: [EliteaAI/elitea_issues#6051]
---
# ELITEA-2781: Oversized Excel Workbook via read_file_from_sharing_link Returns Guidance on Both Primary and 403-Fallback Paths

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Excel pre-parse-estimate size guard added to `read_file_from_sharing_link` produces "content too large" guidance instead of crashing when reading a very large multi-sheet `.xlsx` workbook, and that this guard applies identically on both the normal Graph-authenticated path and the 403 cross-tenant/public-link fallback path.

This test is scoped only to the pre-parse size/row estimate guard on both paths. It does **not** include a `sheet_name`-parameter step — that error-handling mechanic is already covered by the Artifacts-toolkit test `ELITEA-0335` and is intentionally not duplicated here.

## Preconditions

- SharePoint Delegated credential is connected and authenticated
- A sharing link to a very large `.xlsx` file with multiple sheets is available
- A cross-tenant/public link to the same (or an equivalent) large `.xlsx` file is available, one that is known to trigger the Graph 403 → fallback code path

## Test Data

| Field | Value |
|-------|-------|
| File | Large multi-sheet `.xlsx` workbook, sized to trigger the pre-parse row/size estimate guard |
| Path 1 | Normal Graph-authenticated sharing link |
| Path 2 | Cross-tenant/public link that triggers the Graph 403 → fallback path |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `read_file_from_sharing_link` on the large `.xlsx` via the normal (Graph-authenticated) sharing link | "Content too large" guidance is returned; no crash or unhandled exception |
| 2 | Repeat the same read on the cross-tenant/public link that triggers the 403 → fallback path | Identical guidance behavior is returned, confirming the fallback path applies the same Excel pre-parse guard as the primary path |

## Expected Final State

Both the primary Graph-authenticated path and the 403 cross-tenant fallback path return equivalent, well-formed "content too large" guidance for the oversized Excel workbook, with no crash on either path, and the guidance only references parameters the tool actually accepts.

## Pass/Fail Criteria

**Pass:**
- Guidance is returned correctly for the primary path
- Guidance is returned correctly and consistently for the 403-fallback path
- Guidance in both cases matches the tool's actual parameter surface

**Fail:**
- Crash or unhandled exception on either path
- Guidance suggests parameters the tool does not accept
- Fallback path behaves inconsistently with the primary path (e.g. missing the guard, or crashing where the primary path does not)
