---
id: ELITEA-1836
title: "File Tree Behavior – Subfolder Expands and Collapses on Click"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1836: File Tree Behavior – Subfolder Expands and Collapses on Click

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking on a subfolder in the left panel tree expands it to show its files and clicking again collapses it, with the main panel header updating on expansion.

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

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" in the bucket list — verify it expands and shows subfolder "a1" beneath it | "bucket-1" expands, "a1" is shown |
| 3 | Click on subfolder "a1" — verify it expands and shows its files listed beneath it in the left panel tree | "a1" expands and files are shown under it |
| 4 | Verify the main panel header updates to display "bucket-1 > a1" | Breadcrumb shows "bucket-1 > a1" |
| 5 | Click on subfolder "a1" again — verify it collapses and the files are no longer shown beneath it in the left panel tree | "a1" collapses; files are hidden |
| 6 | Verify the left panel tree returns to showing only the "bucket-1" bucket entry with "a1" listed but collapsed | Left panel shows "bucket-1" with collapsed "a1" |

---

## Expected Final State

Subfolder "a1" toggles correctly between expanded (showing files) and collapsed states with each click. The main panel header updates when "a1" is expanded.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Subfolder expands on first click and collapses on second click with correct main panel header updates.

**Fail:**
- Any step produces an error or unexpected result.
- Subfolder does not expand/collapse, or main panel header does not update.
