---
id: ELITEA-1836
title: "File Tree Behavior – Subfolder Expand/Collapse and Breadcrumb/URL Updates on Navigation"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1836: File Tree Behavior – Subfolder Expand/Collapse and Breadcrumb/URL Updates on Navigation

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking a subfolder in the left panel tree expands/collapses it correctly, and that the main panel breadcrumb and browser URL update correctly when navigating between the bucket root and subfolders, including navigating back via the breadcrumb.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" exists with subfolder "a1" containing files.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Subfolder | a1 |

---

## Steps

### Part 1: Expand/Collapse Subfolder

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" in the bucket list — verify it expands and shows subfolder "a1" beneath it | "bucket-1" expands, "a1" is shown |
| 3 | Click on subfolder "a1" — verify it expands and shows its files listed beneath it in the left panel tree | "a1" expands and files are shown under it |
| 4 | Verify the main panel header/breadcrumb updates to display "bucket-1 > a1" | Breadcrumb shows "bucket-1 > a1" |
| 5 | Verify the URL in the browser address bar updates to reflect the subfolder path (e.g. "...?bucket=bucket-1&folder=a1") | URL includes both bucket and folder parameters |
| 6 | Click on subfolder "a1" again — verify it collapses and the files are no longer shown beneath it in the left panel tree | "a1" collapses; files are hidden |
| 7 | Verify the left panel tree returns to showing only the "bucket-1" bucket entry with "a1" listed but collapsed | Left panel shows "bucket-1" with collapsed "a1" |

### Part 2: Breadcrumb Navigation Back to Root

| # | Action | Expected Result |
|---|--------|-----------------|
| 8 | Click on subfolder "a1" again to re-expand it, then click "a1" in the left panel tree to select it | "a1" is selected; breadcrumb shows "bucket-1 > a1" |
| 9 | Click on "bucket-1" in the breadcrumb in the main panel header | Navigation back to root occurs |
| 10 | Verify the main panel navigates back to the root of "bucket-1" | Root level contents are shown |
| 11 | Verify the breadcrumb displays only "bucket-1" | Breadcrumb shows only "bucket-1" |
| 12 | Verify the URL updates back to the root bucket path (e.g. "...?bucket=bucket-1") | URL shows only bucket parameter |

---

## Expected Final State

Subfolder "a1" toggles correctly between expanded and collapsed states. Breadcrumb and URL correctly reflect the current navigation state, and clicking the bucket name in the breadcrumb navigates back to the root and clears the subfolder from the URL.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Subfolder expands/collapses correctly with main panel header updates.
- Breadcrumb and URL update correctly on navigation; breadcrumb click navigates to root.

**Fail:**
- Any step produces an error or unexpected result.
- Subfolder does not expand/collapse, main panel header does not update, or breadcrumb/URL does not update correctly.

---

## Notes

**Source functional tests:** ELITEA-1836, ELITEA-1837

**Regression rationale:** Both tests exercise the same subfolder navigation interaction (click "a1" under "bucket-1"); consolidating avoids duplicated setup while preserving both the expand/collapse checkpoint and the breadcrumb/URL + back-navigation checkpoint.

**Selected checkpoints:**
- Subfolder expand/collapse toggling in left panel tree (ELITEA-1836)
- Breadcrumb and URL update on subfolder navigation (ELITEA-1837)
- Breadcrumb click navigates back to bucket root and URL reverts (ELITEA-1837)
