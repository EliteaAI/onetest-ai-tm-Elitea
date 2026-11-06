---
id: ELITEA-1854
title: "File Preview/Edit – Cancel on Discard Warning Preserves Unsaved Changes (Text File and Markdown Raw Tab)"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1854: File Preview/Edit – Cancel on Discard Warning Preserves Unsaved Changes (Text File and Markdown Raw Tab)

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking "Cancel" on the Discard Warning modal closes the modal and returns to the editor with the unsaved changes still present — for both a plain text file and a Markdown file's Raw tab.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains "machine_learning.py".
- Bucket "bucket-1" contains "project-background.md".

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Text file | machine_learning.py |
| Text edit line | 17 |
| Text temporary change | # temp change |
| Markdown file | project-background.md |
| Markdown temporary change | # Modified Heading |

---

## Steps

### Part 1: Cancel Discard in Text File Editor

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

### Part 2: Cancel Discard in Markdown Raw Tab

| # | Action | Expected Result |
|---|--------|-----------------|
| 10 | Navigate to the Artifacts section and open "project-background.md" via the "View/Edit file" icon | Editor opens |
| 11 | Click the "Raw" tab | Raw tab is active |
| 12 | Modify line 1 to "# Modified Heading" | Change is visible in the editor |
| 13 | Click the "Discard" button | Warning modal opens |
| 14 | Verify the "Warning" modal opens | Modal is visible |
| 15 | Click "Cancel" in the modal | Modal closes |
| 16 | Verify the modal closes | Modal is no longer visible |
| 17 | Verify the editor remains open in "Raw" mode with "# Modified Heading" still present on line 1 | Unsaved change is preserved |
| 18 | Verify the change has not been lost | "# Modified Heading" is visible on line 1 |

---

## Expected Final State

In both the plain-text editor and the Markdown Raw tab, clicking Cancel on the Discard Warning modal closes the modal and returns to the editor with the unsaved change preserved and Save/Discard still active.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Modal closes; editor remains open; unsaved change is preserved, in both the text and Markdown Raw cases.

**Fail:**
- Any step produces an error or unexpected result.
- Change is lost after Cancel, or editor closes, in either case.

---

## Notes

**Source functional tests:** ELITEA-1854, ELITEA-1860

**Regression rationale:** Both tests exercise the identical Cancel-on-Discard-Warning mechanic; the only difference is the file/tab type (plain text editor vs Markdown Raw tab), which doesn't change the underlying modal logic being verified.

**Selected checkpoints:**
- Cancel on Discard Warning preserves unsaved change — text file (ELITEA-1854)
- Cancel on Discard Warning preserves unsaved change — Markdown Raw tab (ELITEA-1860)
