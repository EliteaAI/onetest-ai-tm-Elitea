---
id: ELITEA-3492
title: "Health Tab Health by Event Type Table"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, issue:6736, r-2.0.7, regression]
requirements: [EliteaAI/elitea_issues#6437, EliteaAI/elitea_issues#6736]
---
# ELITEA-3492: Health Tab Health by Event Type Table

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify Health by Event Type table displays correct metrics matching Overview tab.

**Coverage:** Bug #6736 - LLM Calls count should match between Overview and Health tabs.

## Preconditions

- Logged into {{base_url}}
- Project has various event types (api, llm, tool, rpc, socketio)
- Navigate to Settings → Analytics → Health

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Scroll to "Health by Event Type" section. | Table visible with event type breakdown. |
| 2 | Verify table columns. | Columns: EVENT TYPE, TOTAL, ERRORS, ERROR RATE, AVG LATENCY. |
| 3 | Verify expected event types present. | Rows for: rpc, socketio, api, llm, tool. |
| 4 | Verify each event type has status indicator. | Green dot for healthy (0% error), red for issues. |
| 5 | Note "llm" row TOTAL value. | Record the LLM event count. |
| 6 | Navigate to Overview tab. | Overview tab loads. |
| 7 | Compare LLM CALLS card with Health tab llm TOTAL. | Values should match exactly for same date range. |
| 8 | Note "tool" row TOTAL value. | Record the tool event count. |
| 9 | Compare TOOL RUNS card with Health tab tool TOTAL. | Values should match exactly. |
| 10 | Verify ERROR RATE format. | Shows percentage (e.g., "0%", "0.34%"). |
| 11 | Verify AVG LATENCY format. | Shows time (e.g., "156ms", "3.3s"). |

## Pass/Fail Criteria

**Pass:** All event types shown, LLM/Tool counts match Overview tab, error rates calculated correctly.
**Fail:** Counts mismatch between tabs (#6736), missing event types, or wrong error rate.
