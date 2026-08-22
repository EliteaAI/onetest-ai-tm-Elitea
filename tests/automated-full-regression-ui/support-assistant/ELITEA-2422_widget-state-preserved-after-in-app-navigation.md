---
id: ELITEA-2422
title: "Widget state preserved after in-app navigation"
priority: medium
type: functional
module: support-assistant
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:support-assistant]
requirements: []
automation_test_id: tests.ui.support_assistant.test_support_assistant_navigation_persistence.TestSupportAssistantNavigationPersistence.test_widget_state_preserved_after_in_app_navigation
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1651
---

# ELITEA-2422: Widget state preserved after in-app navigation

**Module:** support-assistant · **Priority:** medium · **Type:** functional

**Objective:** Verify that Widget state preserved after in-app navigation. Success is confirmed when send a follow-up message and verify the assistant responds in the same session.

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
| 1 | Open the Support Assistant widget on the Chat page | Target page/section loads successfully. |
| 2 | Send the message "Navigation persistence test" and wait for a response | Action completes without error and produces the expected UI state. |
| 3 | Navigate to the Agents page using the sidebar (do not close the widget) | Target page/section loads successfully. |
| 4 | Verify the widget is still open (or can be reopened via the launcher) with the previous conversation intact | Condition holds as described. |
| 5 | Navigate back to the Chat page | Target page/section loads successfully. |
| 6 | Open the widget if it closed during navigation — verify the previous session messages are still visible | Target page/section loads successfully. |
| 7 | Send a follow-up message and verify the assistant responds in the same session | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Send a follow-up message and verify the assistant responds in the same session.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Widget state preserved after in-app navigation.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
