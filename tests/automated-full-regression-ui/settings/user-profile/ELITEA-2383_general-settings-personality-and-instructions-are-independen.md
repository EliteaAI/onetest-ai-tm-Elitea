---
id: ELITEA-2383
title: "General settings (personality and instructions) are independent of context management toggle state"
priority: high
type: functional
module: settings-user-profile
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_personality_independent_of_context_management.TestPersonalityIndependentOfContextManagement.test_personality_settings_independent_of_context_management
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1969"
---

# ELITEA-2383: General settings (personality and instructions) are independent of context management toggle state

**Module:** settings-user-profile · **Priority:** high · **Type:** functional

**Objective:** Verify that General settings (personality and instructions) are independent of context management toggle state. Success is confirmed when click save — verify the settings save without error.

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
| 1 | Navigate to Personalization | Target page/section loads successfully. |
| 2 | Turn OFF the context management toggle | Action completes without error and produces the expected UI state. |
| 3 | Verify the Default Personality dropdown and Default User Instructions textarea remain editable and are NOT grayed out | Condition holds as described. |
| 4 | Change the Default Personality to "Quirky" | Action completes without error and produces the expected UI state. |
| 5 | Click Save — verify the settings save without error | Control responds; expected next state is shown. |

---

## Expected Final State

Click Save — verify the settings save without error.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: General settings (personality and instructions) are independent of context management toggle state.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
