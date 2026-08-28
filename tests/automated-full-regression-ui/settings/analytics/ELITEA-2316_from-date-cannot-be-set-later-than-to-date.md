---
id: ELITEA-2316
title: "From date cannot be set later than To date"
priority: medium
type: functional
module: settings-analytics
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_analytics_date_filter_controls.TestAnalyticsFromDateConstraint.test_from_date_cannot_be_later_than_to_date
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1958"
---

# ELITEA-2316: From date cannot be set later than To date

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that From date cannot be set later than To date. Success is confirmed when verify the picker prevents the selection and no data changed to the incorrect timespan.

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
| 2 | Set the "To" date to 5 days ago | Action completes without error and produces the expected UI state. |
| 3 | Attempt to set the "From" date to a date after the current "To" date | Action completes without error and produces the expected UI state. |
| 4 | Verify the picker prevents the selection and no data changed to the incorrect timespan | Condition holds as described. |

---

## Expected Final State

Verify the picker prevents the selection and no data changed to the incorrect timespan.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: From date cannot be set later than To date.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
