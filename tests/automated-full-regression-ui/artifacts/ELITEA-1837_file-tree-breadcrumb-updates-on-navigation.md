---
id: ELITEA-1837
title: "File Tree Behavior – Breadcrumb Path Updates on Navigation"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1837: File Tree Behavior – Breadcrumb Path Updates on Navigation

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that the main panel breadcrumb and URL update correctly when navigating between the bucket root and subfolders, and that clicking the bucket name in the breadcrumb navigates back to the root.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" exists with subfolder "a1".

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
| 2 | Click on "bucket-1" in the bucket list | "bucket-1" is selected |
| 3 | Verify the main panel header/breadcrumb displays "bucket-1" | Breadcrumb shows "bucket-1" |
| 4 | Click on subfolder "a1" under "bucket-1" in the left panel | "a1" is selected |
| 5 | Verify the main panel header/breadcrumb updates to "bucket-1 > a1" | Breadcrumb shows "bucket-1 > a1" |
| 6 | Verify the URL in the browser address bar updates to reflect the subfolder path (e.g. "...?bucket=bucket-1&folder=a1") | URL includes both bucket and folder parameters |
| 7 | Click on "bucket-1" in the breadcrumb in the main panel header | Navigation back to root occurs |
| 8 | Verify the main panel navigates back to the root of "bucket-1" | Root level contents are shown |
| 9 | Verify the breadcrumb displays only "bucket-1" | Breadcrumb shows only "bucket-1" |
| 10 | Verify the URL updates back to the root bucket path (e.g. "...?bucket=bucket-1") | URL shows only bucket parameter |

---

## Expected Final State

Breadcrumb and URL correctly reflect the current navigation state. Clicking the bucket name in the breadcrumb navigates back to the root and clears the subfolder from the URL.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Breadcrumb and URL update correctly on navigation; breadcrumb click navigates to root.

**Fail:**
- Any step produces an error or unexpected result.
- Breadcrumb or URL does not update, or clicking breadcrumb does not navigate to root.
