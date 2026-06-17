---
id: ELITEA-0266
title: "Bucket Tree View Expand/Collapse Toggle Cycle — Full Validation"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [bug-area:not-current-release-scope, feat:artifacts, eng:frontend, bug-env:DEV, r-2.0.4, nfr:ui]
requirements: [EliteaAI/elitea_issues#5222]
---
# ELITEA-0266: Bucket Tree View Expand/Collapse Toggle Cycle — Full Validation

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify the complete bucket tree toggle behavior in one cycle: auto-expansion on first click, collapse on second click (the primary fix), and re-expansion on third click, with the file table remaining stable throughout.

**Coverage:**
- Bucket expands its file/folder tree on first click
- File table loads correct bucket contents on selection
- Bucket tree collapses on second click (same selected bucket)
- File table remains populated after collapse
- No error toast or console error during the full cycle
- Bucket re-expands on third click

## Preconditions

- Logged in to {{base_url}} (Private project)
- Bucket `test` exists and contains at least one file
- Bug fix for issue #5222 is applied

## Test Data

- Bucket name: `test`
- Expected file in bucket: `api_client.py` (or any existing file)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the main sidebar | Artifacts page loads; bucket list is visible in the sidebar |
| 2 | Ensure the `test` bucket is not currently expanded (collapse it or reload the page if needed) | `test` bucket shows no tree beneath it |
| 3 | Click the `test` bucket | The tree expands beneath `test` showing its files/folders; file table on the right displays `test` bucket contents |
| 4 | Click the `test` bucket again (it is still selected and expanded) | The tree collapses — no files/folders are visible under `test` in the sidebar; file table still shows `test` contents; no error toast |
| 5 | Click the `test` bucket a third time | The tree expands again, showing the same file/folder structure as in step 3 |
| 6 | Open browser DevTools console and verify no errors were logged during steps 3–5 | No JavaScript errors or network errors in the console |

## Expected Final State

No JavaScript errors or network errors in the console

## Pass/Fail Criteria

**Pass:**
- Tree expands on click 1, collapses on click 2, re-expands on click 3
- File table content is unaffected by the collapse action
- No error toasts or console errors

**Fail:**
- Click 2 does not collapse the tree (bug #5222 not fixed)
- File table clears or changes after collapse
- Any console error or error toast appears
