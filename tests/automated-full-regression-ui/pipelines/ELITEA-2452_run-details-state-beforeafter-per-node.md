---
id: ELITEA-2452
title: "Run Details — State Before/After per Node"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
automation_test_id:
  - tests.ui.pipelines_2.test_pipeline_run_details_state_before_after.test_run_details_state_before_after_per_node
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1273
---

# ELITEA-2452: Run Details — State Before/After per Node

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that Run Details — State Before/After per Node. Success is confirmed when click expand/fullscreen button — verify long values display in full.

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
| 1 | Execute a pipeline with at least 2 state variables and 2+ nodes | Action completes without error and produces the expected UI state. |
| 2 | Open Run Details | Target page/section loads successfully. |
| 3 | Click on a timeline step (node) to select it | Control responds; expected next state is shown. |
| 4 | In STATES section, verify all pipeline state variables appear as expandable rows | Action completes without error and produces the expected UI state. |
| 5 | Click expand button on a state variable row | Control responds; expected next state is shown. |
| 6 | Verify two columns appear: "Before" (value entering the node) and "After" (value leaving the node) | Condition holds as described. |
| 7 | For a variable not modified by this node, verify Before and After show same value | Action completes without error and produces the expected UI state. |
| 8 | For a variable modified by this node, verify After differs from Before | Action completes without error and produces the expected UI state. |
| 9 | Click expand/fullscreen button — verify long values display in full | Control responds; expected next state is shown. |

---

## Expected Final State

Click expand/fullscreen button — verify long values display in full.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Run Details — State Before/After per Node.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
