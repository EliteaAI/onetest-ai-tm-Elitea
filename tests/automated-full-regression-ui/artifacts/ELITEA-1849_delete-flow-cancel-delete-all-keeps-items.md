---
id: ELITEA-1849
title: "Delete Flow – Cancel Delete All Keeps All Items Intact"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1849: Delete Flow – Cancel Delete All Keeps All Items Intact

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking Cancel on the "Delete all files" confirmation modal closes the modal without deleting any items and leaves all file table contents unchanged.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains 4 items: subfolders "a1", "folder-a" and files "sample - Copy.md", "sample.md".

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Items | a1, folder-a, sample - Copy.md, sample.md |
| Pagination | 1 - 4 of 4 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" in the bucket list | Bucket is selected |
| 3 | Click the "Select all" checkbox in the table header row | All 4 items are selected |
| 4 | Verify all 4 items are selected | All rows are checked |
| 5 | Click the "Delete all files" icon | Delete confirmation modal opens |
| 6 | Verify the "Delete confirmation" modal opens with message: "Are you sure to delete all files?" | Modal is visible |
| 7 | Click "Cancel" | Modal closes |
| 8 | Verify the modal closes | Modal is no longer visible |
| 9 | Verify no success notification is displayed | No notification appears |
| 10 | Verify all 4 items ("a1", "folder-a", "sample - Copy.md", "sample.md") remain in the file table unchanged | All items are still present |
| 11 | Verify the pagination still shows "1 - 4 of 4" | Pagination is unchanged |
| 12 | Verify the left panel tree under "bucket-1" remains unchanged | Left panel structure is unchanged |

---

## Expected Final State

All 4 items remain in "bucket-1" unchanged after clicking Cancel. No deletion occurs and no notification is shown.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- No items deleted after Cancel; all items present; pagination unchanged.

**Fail:**
- Any step produces an error or unexpected result.
- Items are deleted after Cancel, or pagination changes.
