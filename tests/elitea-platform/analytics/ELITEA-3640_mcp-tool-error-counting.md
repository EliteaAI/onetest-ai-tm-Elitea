---
id: ELITEA-3640
title: "Analytics — MCP Tool Error Counting"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, mcp, tools, errors, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6572]
---
# ELITEA-3640: Analytics — MCP Tool Error Counting

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that MCP tool errors are tracked separately from successful calls.

**Coverage:**
- Tool errors increment ERRORS column
- Failed calls still count in CALLS column
- Error rate can be derived from ERRORS/CALLS

## Preconditions

- Logged in to {{base_url}}
- Ability to trigger a tool error (e.g., read non-existent file)
- User has access to Analytics > Tools tab

## Test Data

| Field | Value |
|-------|-------|
| Tool | read_file |
| Error Trigger | Request to read non-existent file path |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Analytics > Tools tab | Note read_file CALLS and ERRORS |
| 2 | Execute agent with request to read a non-existent file | Tool call fails with file not found |
| 3 | Navigate to Analytics > Tools tab | read_file row updated |
| 4 | Verify CALLS column | CALLS incremented by 1 (failed call counts) |
| 5 | Verify ERRORS column | ERRORS incremented by 1 |
| 6 | Execute successful read_file call | Tool succeeds |
| 7 | Verify CALLS and ERRORS | CALLS +1, ERRORS unchanged |
| 8 | Calculate error rate: ERRORS / CALLS | Error rate is reasonable |

## Expected Final State

Tool errors are tracked in ERRORS column. Failed calls count toward total CALLS. Error rate trackable.

## Pass/Fail Criteria

**Pass:**
- Failed call increments both CALLS and ERRORS
- Successful call increments only CALLS
- ERRORS ≤ CALLS always

**Fail:**
- Errors not tracked
- Failed call not counted in CALLS
- ERRORS > CALLS (impossible state)
