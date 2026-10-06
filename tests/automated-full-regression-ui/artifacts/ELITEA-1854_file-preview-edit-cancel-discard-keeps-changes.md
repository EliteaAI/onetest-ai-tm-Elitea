---
id: ELITEA-1854
title: "File Preview/Edit – Cancel Discard Warning Returns to Edit Mode with Changes Preserved"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1854: File Preview/Edit – Cancel Discard Warning Returns to Edit Mode with Changes Preserved

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking "Cancel" on the Discard Warning modal closes the modal and returns to the editor with the unsaved changes still present.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains "machine_learning.py".

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| File name | machine_learning.py |
| Edit line | 17 |
| Temporary change | # temp change |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section and open "machine_learning.py" in "bucket-1" via the "View/Edit file" icon | Editor opens |
| 2 | Click into the file content at line 17 and type "# temp change" | "# temp change" appears in the editor |
| 3 | Click the "Discard" button in the top-right | Warning modal opens |
| 4 | Verify the "Warning" modal opens with message: "Are you sure you want to discard changes?" | Modal is visible |
| 5 | Click the "Cancel" button in the modal | Modal closes |
| 6 | Verify the modal closes immediately | Modal is no longer visible |
| 7 | Verify the editor remains open with the unsaved change "# temp change" still visible on line 17 | Change "# temp change" is still present |
| 8 | Verify the user is back in edit mode with all previously made changes intact | Editor is in edit mode with changes preserved |
| 9 | Verify the "Save" and "Discard" buttons remain active in the top-right | Both buttons are active |

---

## Expected Final State

After clicking Cancel on the Warning modal, the editor remains open with "# temp change" preserved on line 17. The editor is in active edit mode.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Modal closes; editor remains open; unsaved change is preserved.

**Fail:**
- Any step produces an error or unexpected result.
- Change is lost after Cancel, or editor closes.
