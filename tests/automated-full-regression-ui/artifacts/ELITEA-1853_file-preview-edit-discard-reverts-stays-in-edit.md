---
id: ELITEA-1853
title: "File Preview/Edit – Discard Changes via Discard Button Reverts to Original and Stays in Edit Mode"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1853: File Preview/Edit – Discard Changes via Discard Button Reverts to Original and Stays in Edit Mode

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking the "Discard" button on unsaved changes shows a Warning modal, and confirming the discard reverts the content to its original state while keeping the editor open.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains "machine_learning.py" with known content at line 17.

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
| 2 | Note the original content on an existing line (e.g. line 17) | Original content is noted |
| 3 | Click into the file content and type "# temp change" on line 17 | "# temp change" appears in the editor |
| 4 | Verify the modified text appears in the editor | Change is visible |
| 5 | Click the "Discard" button in the top-right | Warning modal opens |
| 6 | Verify a "Warning" modal opens with warning icon, title "Warning", message "Are you sure you want to discard changes?", X icon, "Cancel" and "Discard" buttons | Modal shows all required elements |
| 7 | Click the "Discard" button in the modal | Discard action completes |
| 8 | Verify the modal closes | Modal is no longer visible |
| 9 | Verify the file content reverts to the original state — the change "# temp change" is removed | Original content is restored at line 17 |
| 10 | Verify the user remains in edit mode — the editor is still open and active | Editor is still open |
| 11 | Verify the "Save" and "Discard" buttons are still visible in the top-right | Both buttons are still present |
| 12 | Verify no success notification is displayed | No notification appears |

---

## Expected Final State

The unsaved change "# temp change" is discarded and the original content is restored. The editor remains open in edit mode with Save and Discard buttons still visible.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Change reverted; editor remains open; no success notification shown.

**Fail:**
- Any step produces an error or unexpected result.
- Change not reverted, editor closes after discard, or notification appears.
