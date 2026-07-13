---
id: ELITEA-1844
title: "Delete Flow – Delete Single File via Actions Dropdown"
priority: high
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1844: Delete Flow – Delete Single File via Actions Dropdown

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify that a single file can be deleted via the file row actions dropdown with a confirmation modal, and that the file is removed from both the file table and the left panel tree with updated pagination.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains subfolders "a1", "folder-a" and files "sample - Copy.md", "sample.md" (4 items total).

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| File to delete | sample.md |
| File metadata | Markdown, 331 B, 10-07-2026, 06:45 PM |
| Initial pagination | 1 - 4 of 4 |
| Final pagination | 1 - 3 of 3 |
| Delete confirmation message | Are you sure to delete sample.md? It can't be restored. |
| Success notification | The artifacts have been deleted successfully |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" in the bucket list | Bucket is selected |
| 3 | Verify the file table displays items: subfolders "a1", "folder-a" and files "sample - Copy.md", "sample.md" | All 4 items are listed |
| 4 | Verify the pagination at the bottom shows "1 - 4 of 4" | Pagination shows "1 - 4 of 4" |
| 5 | Hover over the "sample.md" file row and click the 3-dot (ellipsis) / actions icon | Dropdown menu appears |
| 6 | Verify a dropdown menu appears with options: "Download" and "Delete" | Both options are visible |
| 7 | Click "Delete" | Delete confirmation modal opens |
| 8 | Verify the "Delete confirmation" modal opens with warning icon, title "Delete confirmation", message "Are you sure to delete sample.md? It can't be restored.", "sample.md" highlighted in blue, X icon, "Cancel" and "Delete" buttons | Modal shows all required elements |
| 9 | Click the "Delete" button | Deletion completes |
| 10 | Verify the modal closes | Modal is no longer visible |
| 11 | Verify a green success notification is displayed: "The artifacts have been deleted successfully" | Success notification appears |
| 12 | Verify "sample.md" is no longer listed in the file table | "sample.md" is absent |
| 13 | Verify the left panel tree under "bucket-1" no longer shows "sample.md" | "sample.md" is removed from left panel |
| 14 | Verify the pagination updates to "1 - 3 of 3" | Pagination shows "1 - 3 of 3" |
| 15 | Verify the remaining items ("a1", "folder-a", "sample - Copy.md") are still listed and unchanged | All 3 remaining items are present |

---

## Expected Final State

"sample.md" is deleted and removed from both the file table and the left panel tree. Pagination updates to "1 - 3 of 3". Remaining 3 items are unchanged.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- File is deleted; success notification shown; pagination updated; remaining items unchanged.

**Fail:**
- Any step produces an error or unexpected result.
- File is not deleted, or pagination does not update, or other files are affected.
