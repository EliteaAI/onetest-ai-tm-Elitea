---
id: ELITEA-1847
title: "Delete Flow – Delete Subfolder via Checkbox Deletes Folder and Its Contents"
priority: high
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1847: Delete Flow – Delete Subfolder via Checkbox Deletes Folder and Its Contents

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify that selecting a subfolder via checkbox and deleting it removes the folder and all its contents from both the file table and the left panel tree.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains subfolders "a1" (with files inside), "folder-a" and files "sample - Copy.md", "sample.md".

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Subfolder to delete | a1 |
| Success notification | The artifacts have been deleted successfully |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" in the bucket list | Bucket is selected |
| 3 | Verify the file table displays subfolders "a1", "folder-a" and files "sample - Copy.md", "sample.md" | All items are listed |
| 4 | Click the checkbox next to subfolder "a1" — verify it becomes checked | "a1" is checked |
| 5 | Verify the delete icon tooltip shows "Delete selected files" | Tooltip text is correct |
| 6 | Click the "Delete selected files" icon | Delete confirmation modal opens |
| 7 | Verify a "Delete confirmation" modal opens with message: "Are you sure to delete selected files?" | Modal is visible |
| 8 | Click the "Delete" button | Deletion completes |
| 9 | Verify a green success notification is displayed: "The artifacts have been deleted successfully" | Success notification appears |
| 10 | Verify subfolder "a1" is no longer listed in the file table | "a1" is absent from file table |
| 11 | Verify subfolder "a1" is no longer shown in the left panel tree under "bucket-1" | "a1" is removed from left panel |
| 12 | Verify all files that were inside "a1" are also removed | No files from "a1" remain |
| 13 | Verify the remaining items ("folder-a", "sample - Copy.md", "sample.md") are still listed unchanged | All 3 remaining items are present |

---

## Expected Final State

Subfolder "a1" and all its contents are permanently deleted. The remaining items in "bucket-1" are unchanged.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Subfolder and its contents deleted; remaining items intact.

**Fail:**
- Any step produces an error or unexpected result.
- Subfolder not deleted, contents remain, or other items are affected.
