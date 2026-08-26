---
id: ELITEA-2274
title: "Discard button reverts unsaved changes"
priority: medium
type: functional
module: settings-project-params
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_project_context_discard_reverts.TestProjectContextDiscardReverts.test_discard_reverts_unsaved_changes
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1799"
---

# ELITEA-2274: Discard button reverts unsaved changes

**Module:** settings-project-params · **Priority:** medium · **Type:** functional

**Objective:** Verify that Discard button reverts unsaved changes. Success is confirmed when verify no changes are persisted.

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
| 1 | Navigate to Settings → Project Context | Target page/section loads successfully. |
| 2 | Note the current content in the Project Background editor | Action completes without error and produces the expected UI state. |
| 3 | Make changes to the content (add or delete text) | Action completes without error and produces the expected UI state. |
| 4 | Click Discard | Control responds; expected next state is shown. |
| 5 | Verify the editor reverts to the previously saved content | Condition holds as described. |
| 6 | Verify no changes are persisted | Condition holds as described. |

---

## Expected Final State

Verify no changes are persisted.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Discard button reverts unsaved changes.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
