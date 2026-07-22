---
id: ELITEA-2326
title: "Hovering over Daily Activity chart on Overview tab shows tooltip with date and series values"
priority: medium
type: functional
module: settings-analytics
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2326: Hovering over Daily Activity chart on Overview tab shows tooltip with date and series values

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Hovering over Daily Activity chart on Overview tab shows tooltip with date and series values. Success is confirmed when move cursor away from the chart — verify the tooltip disappears.

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
| 1 | Navigate to Settings → Analytics → Overview tab | Target page/section loads successfully. |
| 2 | Hover over a data point on the Daily Activity area chart | Action completes without error and produces the expected UI state. |
| 3 | Verify a tooltip appears showing the date and numeric values for both series (Events and Users) | Condition holds as described. |
| 4 | Move to a different data point — verify the tooltip updates | Action completes without error and produces the expected UI state. |
| 5 | Move cursor away from the chart — verify the tooltip disappears | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Move cursor away from the chart — verify the tooltip disappears.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Hovering over Daily Activity chart on Overview tab shows tooltip with date and series values.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
