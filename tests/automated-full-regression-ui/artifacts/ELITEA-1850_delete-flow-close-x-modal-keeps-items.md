---
id: ELITEA-1850
title: "Delete Flow – Close X on Delete Confirmation Modal Keeps Items Intact"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1850: Delete Flow – Close X on Delete Confirmation Modal Keeps Items Intact

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking the X (close) button on the delete confirmation modal closes the modal without deleting any items, and that previously selected items remain checked and unchanged.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains items including selectable files.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" in the bucket list | Bucket is selected |
| 3 | Select one or more items using checkboxes | Selected items are checked |
| 4 | Click the "Delete selected files" icon in the top-right | Delete confirmation modal opens |
| 5 | Verify the "Delete confirmation" modal opens | Modal is visible |
| 6 | Click the X (close) icon in the top-right corner of the modal | Modal closes |
| 7 | Verify the modal closes immediately | Modal is no longer visible |
| 8 | Verify no success notification is displayed | No notification appears |
| 9 | Verify all previously selected items remain in the file table unchanged and files remain checked | All items present and checkboxes still checked |

---

## Expected Final State

No items are deleted after clicking X on the modal. Previously selected items remain in the file table with their checkboxes still checked.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- No items deleted; modal closes via X; selected items remain checked.

**Fail:**
- Any step produces an error or unexpected result.
- Items are deleted after X, or checkboxes are cleared after modal close.
