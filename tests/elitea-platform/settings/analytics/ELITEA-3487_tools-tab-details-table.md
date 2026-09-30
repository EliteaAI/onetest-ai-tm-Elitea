---
id: ELITEA-3487
title: "Tools Tab Tool Details Table"
priority: high
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, issue:6769, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437, EliteaAI/elitea_issues#6769]
---
# ELITEA-3487: Tools Tab Tool Details Table

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify Tool Details table shows complete metrics including Test Tool executions.

**Coverage:** Bug #6769 - Tool run details should display when executed via Test Tool.

## Preconditions

- Logged into {{base_url}}
- Project has tool executions (including Test Tool runs)
- Navigate to Settings → Analytics → Tools

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Scroll to "Tool Details" section. | Table visible with subtitle "X tools". |
| 2 | Verify table columns. | Columns: TOOL, CALLS, USERS, AVG LATENCY, ERRORS. |
| 3 | Verify tool names are displayed. | Tool names like "pyodide_sandbox", "create_file". |
| 4 | Verify CALLS shows integer count. | Total call count per tool. |
| 5 | Verify USERS shows unique user count. | Number with link styling (clickable). |
| 6 | Verify AVG LATENCY format. | Time in seconds/milliseconds (e.g., "2.5s", "218ms"). |
| 7 | Verify ERRORS column. | Integer error count (0 if no errors). |
| 8 | Use search box to filter tools. | Table filters to matching tool names. |
| 9 | Run a tool via "Test Tool" feature. | Tool execution completes. |
| 10 | Refresh Analytics Tools tab. | Test Tool execution appears in CALLS count. |

## Pass/Fail Criteria

**Pass:** Table shows all tools with metrics, Test Tool executions counted.
**Fail:** Columns missing, Test Tool runs not tracked, or search not working.
