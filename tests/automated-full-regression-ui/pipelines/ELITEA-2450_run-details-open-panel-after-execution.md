---
id: ELITEA-2450
title: "Run Details — Open Panel After Execution"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
automation_test_id:
  - tests.ui.pipelines_2.test_pipeline_run_details_panel.test_run_details_panel_opens_after_execution
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1270
---

# ELITEA-2450: Run Details — Open Panel After Execution

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that Run Details — Open Panel After Execution. Success is confirmed when verify panel contains timeline step section and states section.

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
| 1 | Create and execute a pipeline (at least one node) | Operation completes successfully; state updates and confirmation is shown. |
| 2 | After execution completes, click on the run in chat history to open Run Details | Action completes without error and produces the expected UI state. |
| 3 | Verify Run Details panel shows: | Condition holds as described. |
| 4 | Header: "Run N details" (N = run number) | Action completes without error and produces the expected UI state. |
| 5 | "Completed" green badge next to header | Action completes without error and produces the expected UI state. |
| 6 | Trash (delete) icon button | Action completes without error and produces the expected UI state. |
| 7 | Expand/fullscreen button | Action completes without error and produces the expected UI state. |
| 8 | Verify panel contains TIMELINE STEP section and STATES section | Condition holds as described. |

---

## Expected Final State

Verify panel contains TIMELINE STEP section and STATES section.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Run Details — Open Panel After Execution.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
