---
id: ELITEA-1859
title: "File Preview/Edit – Markdown Raw Tab Discard Reverts Changes and Keeps Editor Open"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
automation_test_id:
  - tests.ui.artifacts.test_artifacts_file_preview_markdown_raw_discard.TestArtifactFilePreviewMarkdownRawDiscard.test_markdown_raw_discard_warning_exit_paths
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1696
requirements: []
---

# ELITEA-1859: File Preview/Edit – Markdown Raw Tab Discard Reverts Changes and Keeps Editor Open

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that discarding changes in the Raw tab via the Discard button and confirmation modal reverts the content to original and keeps the editor open in Raw mode.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains "project-background.md" with "# Project Overview" on line 1.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| File name | project-background.md |
| Original heading | # Project Overview |
| Temporary change | # Modified Heading |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section and open "project-background.md" in "bucket-1" via the "View/Edit file" icon | Editor opens |
| 2 | Click the "Raw" tab to switch to raw editing mode | Raw tab is active |
| 3 | Modify line 1: change "# Project Overview" to "# Modified Heading" | Line 1 shows "# Modified Heading" |
| 4 | Click the "Discard" button | Warning modal opens |
| 5 | Verify the "Warning" modal opens with message: "Are you sure you want to discard changes?" | Modal is visible |
| 6 | Click "Discard" in the modal | Discard action completes |
| 7 | Verify the content reverts to the original "# Project Overview" | Original heading is restored |
| 8 | Verify the editor remains open in "Raw" mode with the "Save" and "Discard" buttons still active | Editor is in Raw mode with active buttons |
| 9 | Verify no success notification is displayed | No notification appears |

---

## Expected Final State

The change "# Modified Heading" is reverted to "# Project Overview". The editor remains open in Raw mode with Save and Discard still active.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Change reverted; editor stays in Raw mode; no success notification.

**Fail:**
- Any step produces an error or unexpected result.
- Change not reverted, editor closes, or notification appears.
