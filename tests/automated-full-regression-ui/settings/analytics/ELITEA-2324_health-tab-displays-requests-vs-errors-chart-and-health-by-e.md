---
id: ELITEA-2324
title: "Health tab displays Requests vs Errors chart and Health by Event Type table"
priority: medium
type: functional
module: settings-analytics
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2324: Health tab displays Requests vs Errors chart and Health by Event Type table

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Health tab displays Requests vs Errors chart and Health by Event Type table. Success is confirmed when verify the table has columns: event type, total, errors, error rate, avg latency.

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
| 1 | Navigate to Settings → Analytics → Health tab | Target page/section loads successfully. |
| 2 | Verify a dual-series area chart is shown with Total Requests and Errors series | Condition holds as described. |
| 3 | Verify the Health by Event Type table is shown | Condition holds as described. |
| 4 | Verify the following event types are listed as rows: api, socketio, llm, tool, agent, rpc | Condition holds as described. |
| 5 | Verify the table has columns: Event Type, Total, Errors, Error Rate, Avg Latency | Condition holds as described. |

---

## Expected Final State

Verify the table has columns: Event Type, Total, Errors, Error Rate, Avg Latency.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Health tab displays Requests vs Errors chart and Health by Event Type table.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
