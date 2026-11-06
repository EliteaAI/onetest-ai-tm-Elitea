---
id: ELITEA-1853
title: "File Preview/Edit – Discard Button Reverts Changes and Stays in Edit Mode (Text File and Markdown Raw Tab)"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1853: File Preview/Edit – Discard Button Reverts Changes and Stays in Edit Mode (Text File and Markdown Raw Tab)

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking the "Discard" button on unsaved changes shows a Warning modal, and confirming the discard reverts the content to its original state while keeping the editor open — for both a plain text file and a Markdown file's Raw tab.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains "machine_learning.py" with known content at line 17.
- Bucket "bucket-1" contains "project-background.md" with "# Project Overview" on line 1.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Text file | machine_learning.py |
| Text edit line | 17 |
| Text temporary change | # temp change |
| Markdown file | project-background.md |
| Markdown original heading | # Project Overview |
| Markdown temporary change | # Modified Heading |

---

## Steps

### Part 1: Discard in Text File Editor

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

### Part 2: Discard in Markdown Raw Tab

| # | Action | Expected Result |
|---|--------|-----------------|
| 13 | Navigate to the Artifacts section and open "project-background.md" in "bucket-1" via the "View/Edit file" icon | Editor opens |
| 14 | Click the "Raw" tab to switch to raw editing mode | Raw tab is active |
| 15 | Modify line 1: change "# Project Overview" to "# Modified Heading" | Line 1 shows "# Modified Heading" |
| 16 | Click the "Discard" button | Warning modal opens |
| 17 | Verify the "Warning" modal opens with message: "Are you sure you want to discard changes?" | Modal is visible |
| 18 | Click "Discard" in the modal | Discard action completes |
| 19 | Verify the content reverts to the original "# Project Overview" | Original heading is restored |
| 20 | Verify the editor remains open in "Raw" mode with the "Save" and "Discard" buttons still active | Editor is in Raw mode with active buttons |
| 21 | Verify no success notification is displayed | No notification appears |

---

## Expected Final State

In both the plain-text editor and the Markdown Raw tab, discarding unsaved changes via the Warning modal reverts content to its original state and keeps the editor open with Save/Discard active. No success notification is shown in either case.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Change reverted in both text and Markdown Raw cases; editor remains open; no success notification shown.

**Fail:**
- Any step produces an error or unexpected result.
- Change not reverted, editor closes after discard, or notification appears, in either case.

---

## Notes

**Source functional tests:** ELITEA-1853, ELITEA-1859

**Regression rationale:** Both tests exercise the identical Discard → Warning-modal → confirm → revert mechanic; the only difference is the file/tab type (plain text editor vs Markdown Raw tab), which doesn't change the underlying modal logic being verified.

**Selected checkpoints:**
- Discard reverts unsaved change and keeps editor open — text file (ELITEA-1853)
- Discard reverts unsaved change and keeps editor open — Markdown Raw tab (ELITEA-1859)
