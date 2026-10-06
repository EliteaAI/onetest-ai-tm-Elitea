---
id: ELITEA-2319
title: "Date filter is retained when switching between tabs"
priority: high
type: functional
module: settings-analytics
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2319: Date filter is retained when switching between tabs

**Module:** settings-analytics · **Priority:** high · **Type:** functional

**Objective:** Verify that Date filter is retained when switching between tabs. Success is confirmed when verify from/to values stay consistent with last 30d range on every tab.

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
| 1 | Navigate to Settings → Analytics and click "Last 30d" | Target page/section loads successfully. |
| 2 | Click each tab in sequence: Agents, Tools, Users, Health, Guide, Overview | Control responds; expected next state is shown. |
| 3 | Verify "Last 30d" remains highlighted throughout all tab switches | Condition holds as described. |
| 4 | Verify From/To values stay consistent with Last 30d range on every tab | Condition holds as described. |

---

## Expected Final State

Verify From/To values stay consistent with Last 30d range on every tab.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Date filter is retained when switching between tabs.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
