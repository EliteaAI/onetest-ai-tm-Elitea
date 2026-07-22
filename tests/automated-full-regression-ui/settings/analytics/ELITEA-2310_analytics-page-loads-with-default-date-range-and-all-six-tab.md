---
id: ELITEA-2310
title: "Analytics page loads with default date range and all six tabs visible"
priority: high
type: functional
module: settings-analytics
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2310: Analytics page loads with default date range and all six tabs visible

**Module:** settings-analytics · **Priority:** high · **Type:** functional

**Objective:** Verify that Analytics page loads with default date range and all six tabs visible. Success is confirmed when verify the page does not remain in a permanent loading state.

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
| 2 | Verify the page header shows "Analytics" and the current project name badge | Condition holds as described. |
| 3 | Verify the date filter bar shows four preset buttons: Last 24h, Last 7d, Last 30d, Last 90d | Condition holds as described. |
| 4 | Verify "Last 24d" is active/highlighted by default | Condition holds as described. |
| 5 | Verify the From and To date/time pickers are present and reflect the Last 7d range | Condition holds as described. |
| 6 | Verify the following six tabs are visible: Overview, Agents, Tools, Users, Health, Guide | Condition holds as described. |
| 7 | Verify Overview tab is active and underlined by default | Condition holds as described. |
| 8 | Verify the page does not remain in a permanent loading state | Condition holds as described. |

---

## Expected Final State

Verify the page does not remain in a permanent loading state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Analytics page loads with default date range and all six tabs visible.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
