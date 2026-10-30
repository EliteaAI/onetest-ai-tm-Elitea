---
id: ELITEA-2374
title: "Context management toggle enables and disables token fields"
priority: medium
type: functional
module: settings-user-profile
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_context_management_toggle.TestContextManagementToggle.test_context_management_toggle_enables_disables_fields
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1241
---

# ELITEA-2374: Context management toggle enables and disables token fields

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Context management toggle enables and disables token fields. Success is confirmed when click the toggle back on — verify both fields and summarization become editable again.

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
| 1 | Navigate to Personalization → DEFAULT CONTEXT MANAGEMENT | Target page/section loads successfully. |
| 2 | Verify the "Context window" toggle is present with options Balanced and Full | Condition holds as described. |
| 3 | Verify the "Automatic Summarization" toggle is present with options Balanced and Full | Condition holds as described. |

---

## Expected Final State

Click the toggle back ON — verify both fields and summarization become editable again.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Context management toggle enables and disables token fields.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
