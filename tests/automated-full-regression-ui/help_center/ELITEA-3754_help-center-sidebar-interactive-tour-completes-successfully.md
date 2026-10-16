---
id: ELITEA-3754
title: "Help Center — Sidebar Interactive Tour completes successfully by clicking Next through all steps"
priority: high
type: functional
module: help-center
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:help-center]
requirements: []
automation_test_id:
  - tests.ui.help_center.test_help_center_sidebar_tour.TestHelpCenterSidebarTour.test_sidebar_interactive_tour_completes_via_next
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1163
---

# ELITEA-3754: Help Center — Sidebar Interactive Tour completes successfully by clicking Next through all steps

**Module:** help-center · **Priority:** high · **Type:** functional

**Objective:** Verify that Help Center — Sidebar Interactive Tour completes successfully by clicking Next through all steps. Success is confirmed when click "done!" and verify the modal closes and the user returns to the current project default page view.

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
| 1 | Navigate to Help Center and click "Sidebar Interactive Tour" | Target page/section loads successfully. |
| 2 | Verify the tour starts at step 1/17 | Condition holds as described. |
| 3 | Click the "Next" button | Control responds; expected next state is shown. |
| 4 | Verify the tour advances to step 2/17 and the highlighted sidebar element changes accordingly and Back button becomes active and coloured accordingly | Condition holds as described. |
| 5 | Continue clicking "Next" through all remaining steps | Action completes without error and produces the expected UI state. |
| 6 | Verify each step displays a tooltip with a title, description, and step counter | Condition holds as described. |
| 7 | Verify the "Back" button on intermediate steps returns the user to the previous step and the step counter decrements | Condition holds as described. |
| 8 | Verify the final step (17/17) describes the "Support Assistant" feature with its description | Condition holds as described. |
| 9 | On the final page (17/17) the buttons are Skip Back and Finish, click the "Finish" button | Action completes without error and produces the expected UI state. |
| 10 | Verify the "Tour Complete!" modal appears with a checkmark icon | Condition holds as described. |
| 11 | Verify the modal shows "Keep exploring:" with a "Chat Interactive Tour" option | Condition holds as described. |
| 12 | Verify a "Done!" button is displayed | Condition holds as described. |
| 13 | Click "Done!" and verify the modal closes and the user returns to the current project default page view | Control responds; expected next state is shown. |

---

## Expected Final State

Click "Done!" and verify the modal closes and the user returns to the current project default page view.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Help Center — Sidebar Interactive Tour completes successfully by clicking Next through all steps.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
