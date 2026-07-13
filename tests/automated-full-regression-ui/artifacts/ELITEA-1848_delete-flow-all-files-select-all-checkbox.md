---
id: ELITEA-1848
title: "Delete Flow – Delete All Files and Folders Using Select All Checkbox via Delete All Files Icon"
priority: high
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1848: Delete Flow – Delete All Files and Folders Using Select All Checkbox via Delete All Files Icon

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify that selecting all items with the "Select all" checkbox and deleting them via the "Delete all files" icon removes all files and folders from the bucket, leaving the bucket itself intact with an empty state.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains exactly 4 items: subfolders "a1", "folder-a" and files "sample - Copy.md", "sample.md".

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Items in bucket | a1, folder-a, sample - Copy.md, sample.md (4 items) |
| Confirmation message | Are you sure to delete all files? |
| Success notification | The artifacts have been deleted successfully |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" in the bucket list | Bucket is selected |
| 3 | Verify the file table displays 4 items: "a1", "folder-a", "sample - Copy.md", "sample.md" | All 4 items are listed |
| 4 | Click the "Select all" checkbox in the table header row | All 4 rows become checked |
| 5 | Verify all 4 rows become checked (both subfolders and files) | All rows are checked |
| 6 | Verify the header checkbox shows a fully filled/checked state | Header checkbox is fully checked |
| 7 | Verify the delete icon tooltip shows "Delete all files" | Tooltip shows "Delete all files" |
| 8 | Click the "Delete all files" icon | Delete confirmation modal opens |
| 9 | Verify the "Delete confirmation" modal opens with warning icon, title "Delete confirmation", message "Are you sure to delete all files?" with "all files" highlighted in blue, X icon, "Cancel" and "Delete" buttons | Modal shows all required elements |
| 10 | Click the "Delete" button | Deletion completes |
| 11 | Verify the modal closes | Modal is no longer visible |
| 12 | Verify a green success notification is displayed: "The artifacts have been deleted successfully" | Success notification appears |
| 13 | Verify the file table is empty — no files or subfolders are listed | File table is empty |
| 14 | Verify the main panel shows the empty state | Empty state is displayed |
| 15 | Verify the left panel tree shows "No files in this bucket" under "bucket-1" | Left panel shows empty state message |
| 16 | Verify "bucket-1" still exists in the bucket list (the bucket itself was not deleted) | "bucket-1" remains in bucket list |

---

## Expected Final State

All 4 items are deleted from "bucket-1". The bucket itself remains. Empty state is shown in both panels.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All items deleted; empty state shown; bucket itself persists.

**Fail:**
- Any step produces an error or unexpected result.
- Items not deleted, bucket is also deleted, or empty state not shown.
