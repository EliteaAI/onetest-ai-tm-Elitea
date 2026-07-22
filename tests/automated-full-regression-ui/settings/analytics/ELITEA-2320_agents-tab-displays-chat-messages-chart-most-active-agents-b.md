---
id: ELITEA-2320
title: "Agents tab displays Chat Messages chart, Most Active Agents bar chart, and Agent Activity table"
priority: medium
type: functional
module: settings-analytics
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2320: Agents tab displays Chat Messages chart, Most Active Agents bar chart, and Agent Activity table

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Agents tab displays Chat Messages chart, Most Active Agents bar chart, and Agent Activity table. Success is confirmed when verify a "search by agent name" input is present.

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
| 2 | Verify the "Chat Messages" area chart is shown with subtitle "User messages per day" | Condition holds as described. |
| 3 | Verify the "Most Active Agents" bar chart is shown with subtitle "Top N by events" and agent names on X axis | Condition holds as described. |
| 4 | Verify the "Agent Activity" table is shown with subtitle showing agent count (e.g., "2 agents") | Condition holds as described. |
| 5 | Verify the table has columns: AGENT, EVENTS, USERS, AVG LATENCY, ERRORS | Condition holds as described. |
| 6 | Verify agent names in the table are clickable links | Condition holds as described. |
| 7 | Verify a "Search by agent name" input is present | Condition holds as described. |

---

## Expected Final State

Verify a "Search by agent name" input is present.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Agents tab displays Chat Messages chart, Most Active Agents bar chart, and Agent Activity table.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
