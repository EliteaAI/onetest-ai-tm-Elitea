---
id: ELITEA-2321
title: "Clicking an agent row in Agents tab opens the agent detail view"
priority: medium
type: functional
module: settings-analytics
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2321: Clicking an agent row in Agents tab opens the agent detail view

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Clicking an agent row in Agents tab opens the agent detail view. Success is confirmed when click the back arrow — verify navigation returns to the agent activity table.

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
| 2 | Click on any agent name in the Agent Activity table | Control responds; expected next state is shown. |
| 3 | Verify the view transitions to the agent detail page showing the agent name as title with a back arrow | Condition holds as described. |
| 4 | Verify five KPI cards are shown: Total Events, Unique Users, Avg Latency, Errors, Error Rate | Condition holds as described. |
| 5 | Verify a "Daily Usage" chart is shown | Condition holds as described. |
| 6 | Verify a "Users" panel is shown listing users who used this agent with: USER, EVENTS, AVG LATENCY, ERRORS columns | Condition holds as described. |
| 7 | Verify a "Tools" panel is shown listing tools used by this agent with: TOOL, CALLS columns | Condition holds as described. |
| 8 | If no tools were used, verify "No tool data" message is shown in the Tools panel | Action completes without error and produces the expected UI state. |
| 9 | Click the back arrow — verify navigation returns to the Agent Activity table | Control responds; expected next state is shown. |

---

## Expected Final State

Click the back arrow — verify navigation returns to the Agent Activity table.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Clicking an agent row in Agents tab opens the agent detail view.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
