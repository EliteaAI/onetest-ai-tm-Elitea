---
id: ELITEA-3651
title: "Evaluation Analytics Health Tab Content"
priority: critical
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3651: Evaluation Analytics Health Tab Content

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Health tab displays Event Type table with health metrics for evaluation run.

## Preconditions

- Logged into {{base_url}}
- Evaluation Analytics page open on Health tab

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Evaluation Analytics and click Health tab. | Health tab content displayed. |
| 2 | Verify Event Type table is present. | Table visible with event type breakdown. |
| 3 | Verify EVENT TYPE column. | Event types listed (llm, tool, etc.). |
| 4 | Verify TOTAL column. | Integer counts per event type. |
| 5 | Verify ERRORS column. | Integer error counts. |
| 6 | Verify ERROR RATE column. | Percentage format (e.g., "0%", "0.34%"). |
| 7 | Verify AVG LATENCY column. | Time format (e.g., "156ms", "3.3s"). |
| 8 | Verify status indicators. | Green dot for 0% error, red for >0%. |

## Pass/Fail Criteria

**Pass:** Event Type table with 5 columns, correct status indicators.
**Fail:** Columns missing, wrong formats, or incorrect indicators.
