---
id: ELITEA-2377
title: "Summarization toggle enables and disables summarization fields"
priority: medium
type: functional
module: settings-user-profile
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_context_management_toggle.TestContextManagementToggle.test_automatic_summarization_toggle_enables_disables_own_fields
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1243
---

# ELITEA-2377: Summarization toggle enables and disables summarization fields

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Summarization toggle enables and disables summarization fields. Success is confirmed when toggle back on — verify fields are editable again.

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
| 1 | Navigate to  Personalization → DEFAULT SUMMARIZATION | Target page/section loads successfully. |
| 2 | Ensure Context Management is enabled (required for summarization to be active) | Condition holds as described. |
| 3 | Verify the "Enable automatic summarization" toggle is present | Condition holds as described. |
| 4 | Verify when toggle is ON: Summarization Instructions textarea and Target Summary Tokens field are editable | Condition holds as described. |
| 5 | Verify default value: Target Summary Tokens = 4096 | Condition holds as described. |
| 6 | Click the toggle to turn it OFF | Control responds; expected next state is shown. |
| 7 | Verify Summarization Instructions and Target Summary Tokens become grayed out / uneditable | Condition holds as described. |
| 8 | Toggle back ON — verify fields are editable again | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Toggle back ON — verify fields are editable again.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Summarization toggle enables and disables summarization fields.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
