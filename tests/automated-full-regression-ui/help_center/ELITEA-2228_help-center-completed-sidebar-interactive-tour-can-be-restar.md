---
id: ELITEA-2228
title: "Help Center — completed Sidebar Interactive Tour can be restarted from Help Center"
priority: medium
type: functional
module: help-center
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:help-center]
requirements: []
automation_test_id:
  - tests.ui.help_center.test_help_center_sidebar_tour.TestHelpCenterSidebarTourExtras.test_sidebar_interactive_tour_restarts_after_completion
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1495
---

# ELITEA-2228: Help Center — completed Sidebar Interactive Tour can be restarted from Help Center

**Module:** help-center · **Priority:** medium · **Type:** functional

**Objective:** Verify that Help Center — completed Sidebar Interactive Tour can be restarted from Help Center. Success is confirmed when verify all steps are accessible again from the beginning.

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
| 1 | Complete the Sidebar Interactive Tour fully by clicking through all steps and clicking "Done!" | Action completes without error and produces the expected UI state. |
| 2 | Navigate back to Help Center | Target page/section loads successfully. |
| 3 | Locate the INTERACTIVE TOURS card | Action completes without error and produces the expected UI state. |
| 4 | Verify the "Sidebar Interactive Tour" link is still visible and clickable | Condition holds as described. |
| 5 | Click "Sidebar Interactive Tour" again | Control responds; expected next state is shown. |
| 6 | Verify the tour restarts from step 1/17 | Condition holds as described. |
| 7 | Verify all steps are accessible again from the beginning | Condition holds as described. |

---

## Expected Final State

Verify all steps are accessible again from the beginning.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Help Center — completed Sidebar Interactive Tour can be restarted from Help Center.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
