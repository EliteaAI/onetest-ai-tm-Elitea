---
id: ELITEA-2315
title: "Custom From/To date range filters data"
priority: medium
type: functional
module: settings-analytics
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2315: Custom From/To date range filters data

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Custom From/To date range filters data. Success is confirmed when verify the charts and tables update to reflect the custom date range.

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
| 1 | Navigate to Settings → Analytics | Target page/section loads successfully. |
| 2 | Click the "From" calendar icon and select a date/time in the past | Control responds; expected next state is shown. |
| 3 | Click "Ok" to confirm | Control responds; expected next state is shown. |
| 4 | Click the "To" calendar icon and select a date/time after the From value | Control responds; expected next state is shown. |
| 5 | Click "Ok" to confirm | Control responds; expected next state is shown. |
| 6 | Verify the From and To fields display the selected values | Condition holds as described. |
| 7 | Verify the charts and tables update to reflect the custom date range | Condition holds as described. |

---

## Expected Final State

Verify the charts and tables update to reflect the custom date range.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Custom From/To date range filters data.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
