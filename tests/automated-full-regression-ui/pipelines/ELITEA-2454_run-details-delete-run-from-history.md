---
id: ELITEA-2454
title: "Run Details — Delete Run from History"
priority: high
type: functional
module: pipelines
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
automation_test_id:
  - tests.ui.pipelines.test_pipeline_run_details_delete_run_from_history.test_run_details_delete_run_from_history
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1390
---

# ELITEA-2454: Run Details — Delete Run from History

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that Run Details — Delete Run from History. Success is confirmed when re-open run history — verify the deleted run no longer appears.

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
| 1 | Execute a pipeline at least 2 times to have multiple runs in history | Action completes without error and produces the expected UI state. |
| 2 | Open Run Details for one run — note the run number (e.g., "Run 3 details") | Target page/section loads successfully. |
| 3 | Click the trash/delete icon button in the Run Details header | Control responds; expected next state is shown. |
| 4 | Confirm deletion if prompted | Operation completes successfully; state updates and confirmation is shown. |
| 5 | Verify the run is removed from run history | Condition holds as described. |
| 6 | Verify other runs remain unaffected | Condition holds as described. |
| 7 | Re-open run history — verify the deleted run no longer appears | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Re-open run history — verify the deleted run no longer appears.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Run Details — Delete Run from History.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
