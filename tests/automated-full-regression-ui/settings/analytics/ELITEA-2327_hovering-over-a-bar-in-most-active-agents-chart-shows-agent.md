---
id: ELITEA-2327
title: "Hovering over a bar in Most Active Agents chart shows agent name and event count"
priority: medium
type: functional
module: settings-analytics
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2327: Hovering over a bar in Most Active Agents chart shows agent name and event count

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Hovering over a bar in Most Active Agents chart shows agent name and event count. Success is confirmed when move to a different bar — verify the tooltip updates with the correct agent and value.

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
| 1 | Navigate to Settings → Analytics → Agents tab | Target page/section loads successfully. |
| 2 | Hover over any bar in the Most Active Agents bar chart | Action completes without error and produces the expected UI state. |
| 3 | Verify a tooltip appears showing the agent name and its event count value | Condition holds as described. |
| 4 | Move to a different bar — verify the tooltip updates with the correct agent and value | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Move to a different bar — verify the tooltip updates with the correct agent and value.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Hovering over a bar in Most Active Agents chart shows agent name and event count.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
