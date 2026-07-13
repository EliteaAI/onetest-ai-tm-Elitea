---
id: ELITEA-1846
title: "Delete Flow – Delete Multiple Selected Files (Partial Selection) via Delete Selected Files Icon"
priority: high
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1846: Delete Flow – Delete Multiple Selected Files (Partial Selection) via Delete Selected Files Icon

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify that selecting a subset of files and clicking the "Delete selected files" icon triggers a confirmation modal, and successfully deletes only the selected files while leaving unselected items intact.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains exactly: subfolders "a1", "folder-a" and files "sample - Copy.md", "sample.md" (4 items total).

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Files to delete | sample - Copy.md, sample.md |
| Items to keep | a1, folder-a |
| Confirmation message | Are you sure to delete selected files? |
| Success notification | The artifacts have been deleted successfully |
| Final pagination | 1 - 2 of 2 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" in the bucket list | Bucket is selected |
| 3 | Verify the file table displays 4 items: "a1", "folder-a", "sample - Copy.md", "sample.md" | All 4 items are listed |
| 4 | Click the checkbox next to "sample - Copy.md" — verify it becomes checked | "sample - Copy.md" is checked |
| 5 | Click the checkbox next to "sample.md" — verify it becomes checked | "sample.md" is checked |
| 6 | Verify subfolders "a1" and "folder-a" remain unchecked | Both subfolders are unchecked |
| 7 | Verify the header checkbox shows an indeterminate (minus/dash) state | Header checkbox shows indeterminate state |
| 8 | Verify the delete icon tooltip shows "Delete selected files" | Tooltip text is correct |
| 9 | Click the "Delete selected files" icon | Delete confirmation modal opens |
| 10 | Verify the "Delete confirmation" modal opens with warning icon, title "Delete confirmation", message "Are you sure to delete selected files?" with "selected files" highlighted in blue, X icon, "Cancel" and "Delete" buttons | Modal shows all required elements |
| 11 | Click the "Delete" button | Deletion completes |
| 12 | Verify the modal closes | Modal is no longer visible |
| 13 | Verify a green success notification is displayed: "The artifacts have been deleted successfully" | Success notification appears |
| 14 | Verify "sample - Copy.md" and "sample.md" are no longer listed in the file table | Both files are removed |
| 15 | Verify the left panel tree under "bucket-1" no longer shows "sample - Copy.md" or "sample.md" | Files removed from left panel |
| 16 | Verify subfolders "a1" and "folder-a" are still listed and unchanged | Both subfolders remain |
| 17 | Verify the pagination updates to "1 - 2 of 2" | Pagination shows "1 - 2 of 2" |

---

## Expected Final State

Only "sample - Copy.md" and "sample.md" are deleted. Subfolders "a1" and "folder-a" remain. Pagination updates to "1 - 2 of 2".

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Only selected files deleted; subfolders intact; pagination updated.

**Fail:**
- Any step produces an error or unexpected result.
- Wrong files deleted, subfolders affected, or pagination incorrect.
