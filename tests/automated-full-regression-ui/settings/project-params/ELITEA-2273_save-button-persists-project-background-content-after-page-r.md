---
id: ELITEA-2273
title: "Save button persists Project Background content after page reload"
priority: medium
type: functional
module: settings-project-params
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_project_context_save_persists.TestProjectContextSavePersists.test_save_persists_project_context_after_reload
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1799"
---

# ELITEA-2273: Save button persists Project Background content after page reload

**Module:** settings-project-params · **Priority:** medium · **Type:** functional

**Objective:** Verify that Save button persists Project Background content after page reload. Success is confirmed when verify the project background editor shows the previously entered content.

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
| 2 | Enter project context text: "## Project Overview. This is a test project." | Field accepts the input and displays the entered value. |
| 3 | Click Save | Control responds; expected next state is shown. |
| 4 | Verify a success confirmation is shown | Condition holds as described. |
| 5 | Reload the page | Action completes without error and produces the expected UI state. |
| 6 | Verify the Project Background editor shows the previously entered content | Condition holds as described. |

---

## Expected Final State

Verify the Project Background editor shows the previously entered content.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Save button persists Project Background content after page reload.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
