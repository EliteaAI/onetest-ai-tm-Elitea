---
id: ELITEA-1844
title: "Delete Flow: Single file, delete all, cancel/close variations"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1844: Delete Flow: Single file, delete all, cancel/close variations

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify comprehensive delete functionality: single file deletion, bulk delete all with Select All checkbox, and Cancel/Close X variations for both single and bulk delete confirmation modals. Verify pagination updates and empty state display.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains exactly 4 items: subfolders "a1", "folder-a" and files "sample.md" (Markdown, 331 B), "sample - Copy.md".

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Items in bucket | a1, folder-a, sample.md, sample - Copy.md (4 items) |
| Initial pagination | 1 - 4 of 4 |
| After 1 deletion | 1 - 3 of 3 |
| Delete confirmation (single) | Are you sure to delete sample.md? It can't be restored. |
| Delete confirmation (all) | Are you sure to delete all files? |
| Success notification | The artifacts have been deleted successfully |

---

## Steps

### Part 1: Cancel Single File Delete

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Artifacts section | Artifacts page loads |
| 2 | Click on "bucket-1" in bucket list | Bucket selected; 4 items visible |
| 3 | Verify pagination shows "1 - 4 of 4" | Pagination correct |
| 4 | Hover over "sample.md" row, click 3-dot menu | Dropdown menu appears with Download, Delete |
| 5 | Click Delete | Delete confirmation modal opens |
| 6 | Verify modal shows: warning icon, title "Delete confirmation", message "Are you sure to delete sample.md? It can't be restored.", filename highlighted, X button, Cancel and Delete buttons | Modal displays all elements |
| 7 | Click Cancel button | Modal closes |
| 8 | Verify modal is closed | Modal no longer visible |
| 9 | Verify no success notification appears | No notification |
| 10 | Verify "sample.md" is still present in file table with metadata unchanged (Markdown, 331 B) | File intact |
| 11 | Verify pagination still shows "1 - 4 of 4" | Pagination unchanged |

### Part 2: Close X Button on Single File Delete

| # | Action | Expected Result |
|---|--------|-----------------|
| 12 | Hover over "sample.md" row, click 3-dot menu | Dropdown appears |
| 13 | Click Delete | Delete confirmation modal opens |
| 14 | Click X (close) button in top-right of modal | Modal closes |
| 15 | Verify modal is closed | Modal no longer visible |
| 16 | Verify no success notification appears | No notification |
| 17 | Verify "sample.md" is still present | File intact |

### Part 3: Confirm Single File Delete

| # | Action | Expected Result |
|---|--------|-----------------|
| 18 | Hover over "sample.md" row, click 3-dot menu, click Delete | Delete confirmation modal opens |
| 19 | Click Delete button | Deletion executes |
| 20 | Verify modal closes | Modal no longer visible |
| 21 | Verify green success notification: "The artifacts have been deleted successfully" | Success notification appears |
| 22 | Verify "sample.md" is no longer listed in file table | File removed |
| 23 | Verify "sample.md" removed from left panel tree under "bucket-1" | File removed from tree |
| 24 | Verify pagination updates to "1 - 3 of 3" | Pagination updated |
| 25 | Verify remaining 3 items (a1, folder-a, sample - Copy.md) are unchanged | Other items intact |

### Part 4: Cancel Delete All

| # | Action | Expected Result |
|---|--------|-----------------|
| 26 | Click "Select all" checkbox in table header | All 3 rows become checked |
| 27 | Verify all 3 items are checked; header checkbox is fully checked | All selected |
| 28 | Verify delete icon tooltip shows "Delete all files" | Tooltip correct |
| 29 | Click "Delete all files" icon | Delete confirmation modal opens |
| 30 | Verify modal shows: "Delete confirmation" title, message "Are you sure to delete all files?" with "all files" highlighted, X button, Cancel and Delete buttons | Modal displays correctly |
| 31 | Click Cancel button | Modal closes |
| 32 | Verify modal is closed | Modal no longer visible |
| 33 | Verify no success notification appears | No notification |
| 34 | Verify all 3 items still present in file table | All items intact |
| 35 | Verify pagination still shows "1 - 3 of 3" | Pagination unchanged |

### Part 5: Close X Button on Delete All

| # | Action | Expected Result |
|---|--------|-----------------|
| 36 | Verify "Select all" checkbox is still checked (from step 26) | All items selected |
| 37 | Click "Delete all files" icon | Delete confirmation modal opens |
| 38 | Click X (close) button in modal | Modal closes |
| 39 | Verify no success notification appears | No notification |
| 40 | Verify all 3 items still present | All items intact |

### Part 6: Confirm Delete All

| # | Action | Expected Result |
|---|--------|-----------------|
| 41 | Click "Select all" checkbox again (ensure all selected) | All 3 items checked |
| 42 | Click "Delete all files" icon | Delete confirmation modal opens |
| 43 | Click Delete button | Deletion executes |
| 44 | Verify modal closes | Modal no longer visible |
| 45 | Verify green success notification: "The artifacts have been deleted successfully" | Success notification appears |
| 46 | Verify file table is empty (no files or subfolders) | Table is empty |
| 47 | Verify main panel shows empty state with "Upload files" button | Empty state displayed |
| 48 | Verify left panel tree shows "No files in this bucket" under "bucket-1" | Left panel shows empty message |
| 49 | Verify "bucket-1" still exists in bucket list (bucket itself not deleted) | Bucket persists |

---

## Expected Final State

- Cancel and Close X buttons properly prevent deletion for both single and bulk operations
- Single file deletion works correctly with pagination update
- Delete All removes all items, displays empty state, but preserves bucket
- All success notifications and confirmations function correctly

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Cancel/Close X prevent deletion; no notifications when cancelled.
- Single delete removes file and updates pagination.
- Delete All removes all items, shows empty state, bucket persists.

**Fail:**
- Any step produces an error or unexpected result.
- Deletion occurs after Cancel/Close X, pagination incorrect, empty state not shown, or bucket deleted.

---

## Notes

**Source functional tests:** ELITEA-1844, ELITEA-1845, ELITEA-1848, ELITEA-1849, ELITEA-1850

**Regression rationale:** Consolidates all delete flow variations (single/bulk, confirm/cancel/close) into a comprehensive test covering the complete deletion workflow with all edge cases and cancellation paths.

**Selected checkpoints:**
- Single file delete with Cancel (ELITEA-1845)
- Single file delete with Close X (ELITEA-1850)
- Single file delete confirmed (ELITEA-1844)
- Delete all with Cancel (ELITEA-1849)
- Delete all with Close X (ELITEA-1850)
- Delete all confirmed with empty state (ELITEA-1848)
- Pagination updates after deletions
- Bucket persistence after delete all
