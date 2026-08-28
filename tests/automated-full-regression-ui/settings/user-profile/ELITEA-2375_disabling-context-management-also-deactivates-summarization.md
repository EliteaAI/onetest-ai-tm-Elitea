---
id: ELITEA-2375
title: "Disabling context management also deactivates summarization regardless of summarization toggle state"
priority: medium
type: functional
module: settings-user-profile
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_context_management_toggle.TestContextManagementToggle.test_disabling_context_management_deactivates_summarization
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1969"
---

# ELITEA-2375: Disabling context management also deactivates summarization regardless of summarization toggle state

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Disabling context management also deactivates summarization regardless of summarization toggle state. Success is confirmed when verify summarization settings become active again.

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
| 1 | Navigate to  Personalization | Target page/section loads successfully. |
| 2 | Enable both context management and summarization toggles | Action completes without error and produces the expected UI state. |
| 3 | Turn context management toggle OFF | Action completes without error and produces the expected UI state. |
| 4 | Verify the summarization toggle appears grayed out / inactive | Condition holds as described. |
| 5 | Verify the summarization fields (Summarization Instructions, Target Summary Tokens) are uneditable | Condition holds as described. |
| 6 | Turn context management back ON | Action completes without error and produces the expected UI state. |
| 7 | Verify summarization settings become active again | Condition holds as described. |

---

## Expected Final State

Verify summarization settings become active again.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Disabling context management also deactivates summarization regardless of summarization toggle state.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
