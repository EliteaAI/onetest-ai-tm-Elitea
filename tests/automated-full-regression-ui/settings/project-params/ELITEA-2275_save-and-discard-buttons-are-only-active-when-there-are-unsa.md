---
id: ELITEA-2275
title: "Save and Discard buttons are only active when there are unsaved changes"
priority: medium
type: functional
module: settings-project-params
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_project_context_save_discard_dirty_state.TestProjectContextSaveDiscardDirtyState.test_save_and_discard_active_only_with_unsaved_changes
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1799"
---

# ELITEA-2275: Save and Discard buttons are only active when there are unsaved changes

**Module:** settings-project-params · **Priority:** medium · **Type:** functional

**Objective:** Verify that Save and Discard buttons are only active when there are unsaved changes. Success is confirmed when click discard — verify buttons become inactive again.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Project Context with existing saved content | Target page/section loads successfully. |
| 2 | Verify the Save and Discard buttons are inactive/disabled when no changes have been made | Condition holds as described. |
| 3 | Make a change in the Project Background editor | Action completes without error and produces the expected UI state. |
| 4 | Verify the Save and Discard buttons become active/enabled | Condition holds as described. |
| 5 | Click Discard — verify buttons become inactive again | Control responds; expected next state is shown. |

---

## Expected Final State

Click Discard — verify buttons become inactive again.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Save and Discard buttons are only active when there are unsaved changes.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
