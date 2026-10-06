---
id: ELITEA-1845
title: "Delete Flow – Delete Single File via Actions Dropdown – Cancel Keeps File Intact"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1845: Delete Flow – Delete Single File via Actions Dropdown – Cancel Keeps File Intact

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking Cancel on the delete confirmation modal closes the modal without deleting the file and leaves all file table metadata unchanged.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains "sample.md" (Markdown, 331 B, 10-07-2026, 06:45 PM) as one of 4 items.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| File to attempt delete | sample.md |
| File metadata | Markdown, 331 B, 10-07-2026, 06:45 PM |
| Pagination | 1 - 4 of 4 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" in the bucket list | Bucket is selected |
| 3 | Hover over the "sample.md" file row and click the 3-dot (ellipsis) / actions icon | Dropdown menu appears |
| 4 | Click "Delete" | Delete confirmation modal opens |
| 5 | Verify the "Delete confirmation" modal opens with message: "Are you sure to delete sample.md? It can't be restored." | Modal is visible with correct message |
| 6 | Click "Cancel" | Modal closes |
| 7 | Verify the modal closes | Modal is no longer visible |
| 8 | Verify no success notification is displayed | No notification appears |
| 9 | Verify "sample.md" is still listed in the file table with all its values unchanged (Markdown, 331 B, 10-07-2026, 06:45 PM) | "sample.md" is still present with original metadata |
| 10 | Verify the pagination still shows "1 - 4 of 4" | Pagination is unchanged |

---

## Expected Final State

"sample.md" is not deleted after clicking Cancel. All file metadata is unchanged and pagination remains at "1 - 4 of 4".

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- File remains with unchanged metadata; no notification; pagination unchanged.

**Fail:**
- Any step produces an error or unexpected result.
- File is deleted after Cancel, metadata changes, or pagination updates.
