---
id: ELITEA-1855
title: "File Preview/Edit – Close Editor via X Button Without Saving Does Not Persist Changes"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
automation_test_id:
  - tests.ui.artifacts.test_artifacts_file_preview_close_x_unsaved.TestArtifactFilePreviewCloseXUnsaved.test_close_editor_via_x_does_not_persist_changes
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1696
requirements: []
---

# ELITEA-1855: File Preview/Edit – Close Editor via X Button Without Saving Does Not Persist Changes

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that closing the editor via the X button without saving discards the unsaved changes, and that the file's "Last update" timestamp remains unchanged.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains "machine_learning.py" with a known "Last update" timestamp.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| File name | machine_learning.py |
| Edit line | 17 |
| Unsaved text | # unsaved change |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section and open "machine_learning.py" in "bucket-1" via the "View/Edit file" icon | Editor opens |
| 2 | Click into the file content at line 17 and type "# unsaved change" | "# unsaved change" appears in the editor |
| 3 | Click the X (close) icon to close the editor panel | Editor closes |
| 4 | Verify the editor closes and the main panel returns to the "bucket-1" file table | File table is shown |
| 5 | Verify the "Last update" timestamp for "machine_learning.py" has NOT changed | Timestamp is identical to before editing |
| 6 | Reopen "machine_learning.py" — verify the unsaved change "# unsaved change" is not present | "# unsaved change" is absent; original content is shown |

---

## Expected Final State

Closing the editor via X without saving discards "# unsaved change". The file content and "Last update" timestamp are unchanged.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Unsaved change is not persisted; timestamp is unchanged; original content on reopen.

**Fail:**
- Any step produces an error or unexpected result.
- Unsaved change is saved, or timestamp changes after close without save.
