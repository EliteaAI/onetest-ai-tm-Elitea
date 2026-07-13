---
id: ELITEA-1860
title: "File Preview/Edit – Markdown Raw Tab Cancel Discard Returns to Raw Edit with Changes Intact"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1860: File Preview/Edit – Markdown Raw Tab Cancel Discard Returns to Raw Edit with Changes Intact

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking Cancel on the Discard Warning modal in Raw edit mode closes the modal and returns to the editor with the unsaved change still present.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains "project-background.md".

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| File name | project-background.md |
| Temporary change | # Modified Heading |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section and open "project-background.md" via the "View/Edit file" icon | Editor opens |
| 2 | Click the "Raw" tab | Raw tab is active |
| 3 | Modify line 1 to "# Modified Heading" | Change is visible in the editor |
| 4 | Click the "Discard" button | Warning modal opens |
| 5 | Verify the "Warning" modal opens | Modal is visible |
| 6 | Click "Cancel" in the modal | Modal closes |
| 7 | Verify the modal closes | Modal is no longer visible |
| 8 | Verify the editor remains open in "Raw" mode with "# Modified Heading" still present on line 1 | Unsaved change is preserved |
| 9 | Verify the change has not been lost | "# Modified Heading" is visible on line 1 |

---

## Expected Final State

After clicking Cancel on the Warning modal, the editor remains open in Raw mode with "# Modified Heading" preserved. No data loss occurred.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Modal closes; editor stays in Raw mode; change preserved.

**Fail:**
- Any step produces an error or unexpected result.
- Change lost after Cancel, or editor closes.
