---
id: ELITEA-2230
title: "Help Center — Back button navigates to previous step during Interactive Tour"
priority: medium
type: functional
module: help-center
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:help-center]
requirements: []
---

# ELITEA-2230: Help Center — Back button navigates to previous step during Interactive Tour

**Module:** help-center · **Priority:** medium · **Type:** functional

**Objective:** Verify that Help Center — Back button navigates to previous step during Interactive Tour. Success is confirmed when verify the "back" button is disabled or inactive on step 1/17.

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
| 2 | Click "Next" to advance to step 2/17 | Control responds; expected next state is shown. |
| 3 | Verify the tour is on step 2/17 and the step counter shows "2 / 17" | Condition holds as described. |
| 4 | Click the "Back" button | Control responds; expected next state is shown. |
| 5 | Verify the tour returns to step 1/17 | Condition holds as described. |
| 6 | Verify the tooltip content matches the content of step 1 | Condition holds as described. |
| 7 | Verify the step counter updates to "1 / 17" | Condition holds as described. |
| 8 | Verify the "Back" button is disabled or inactive on step 1/17 | Condition holds as described. |

---

## Expected Final State

Verify the "Back" button is disabled or inactive on step 1/17.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Help Center — Back button navigates to previous step during Interactive Tour.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
