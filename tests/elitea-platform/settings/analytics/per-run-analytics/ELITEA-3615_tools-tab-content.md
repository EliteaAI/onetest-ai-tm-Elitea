---
id: ELITEA-3615
title: "Tools Tab Content - Table and Data Accuracy"
priority: critical
type: functional
module: per-run-analytics
status: ready
execution_type: manual
tags: [feat:analytics, eng:frontend, issue:6816, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3615: Tools Tab Content - Table and Data Accuracy

**Module:** Per-Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Tools tab displays Tool Details table with correct columns and run-specific data.

## Preconditions

- Logged into {{base_url}}
- Per-Run Analytics page open for run with known tool usage

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Per-Run Analytics and click Tools tab. | Tools tab content displayed. |
| 2 | Verify Tool Details table is present. | Table visible with subtitle "X tools". |
| 3 | Verify TOOL column. | Tool names displayed. |
| 4 | Verify CALLS column. | Integer call counts per tool. |
| 5 | Verify USERS column. | User count per tool. |
| 6 | Verify AVG LATENCY column. | Time in "Xs" or "Yms" format. |
| 7 | Verify ERRORS column. | Integer error counts (0 if no errors). |
| 8 | Verify tools listed match what was invoked in this run. | Only tools from this specific run appear. |
| 9 | Verify call counts are run-scoped (not project-wide). | Counts match single run execution. |

## Pass/Fail Criteria

**Pass:** Tool Details table with 5 columns, run-specific data only.
**Fail:** Columns missing, wrong data, or project-wide data shown.
