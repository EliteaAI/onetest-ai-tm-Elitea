---
id: ELITEA-4423
title: "Verify Tool Details table displays accurate data when Tools tab visible"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, tools, data-accuracy]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- Run has tool usage (Tools tab is visible)
- User is on Tools tab of analytics page

## Test Data

| Field | Value |
|-------|-------|
| Table Columns | TOOL, CALLS, USERS, AVG LATENCY, ERRORS |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On analytics page, click "Tools" tab | Tools tab opens |
| 2 | Observe "Tool Details" table | Table visible with data |
| 3 | Check table columns | Columns: TOOL, CALLS, USERS, AVG LATENCY, ERRORS |
| 4 | Verify all tools used in run are listed by name | All tool names appear in TOOL column |
| 5 | Verify CALLS column | Total number of times each tool was invoked |
| 6 | Verify USERS column | Count of unique users who used each tool |
| 7 | Verify AVG LATENCY column | Average execution time per tool (in ms) |
| 8 | Verify ERRORS column | Count of failed tool calls |
| 9 | Cross-reference with usage_event tool_call rows | Data reconciles with DB values |
| 10 | Verify calculations: CALLS >= USERS (unless all shared) | Logical consistency |

## Expected Final State

Tool Details table displays:
- All tools used in the run listed by name
- CALLS: total invocations per tool
- USERS: unique user count per tool
- AVG LATENCY: average execution time (ms)
- ERRORS: failed call count per tool
- Data reconciles with usage_event table

## Pass/Fail Criteria

**Pass:**
- All tools used in run are listed
- CALLS count accurate
- USERS count accurate (unique users)
- AVG LATENCY calculated correctly
- ERRORS count accurate
- Data matches usage_event tool_call rows
- Values logically consistent

**Fail:**
- Missing tools
- CALLS count incorrect
- USERS count incorrect
- AVG LATENCY wrong or missing
- ERRORS count incorrect
- Data doesn't match usage_event table
- Logical inconsistencies
