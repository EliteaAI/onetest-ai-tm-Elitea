---
id: ELITEA-3641
title: "Analytics — MCP Tool Unique Users Count Tracking"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, mcp, tools, users, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6572]
---
# ELITEA-3641: Analytics — MCP Tool Unique Users Count Tracking

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that the USERS column in Tool Details tracks unique users who have used each tool.

**Coverage:**
- USERS shows count of unique users
- Same user calling tool multiple times = 1 user
- Different users calling same tool = incremented user count

## Preconditions

- Logged in to {{base_url}}
- At least one other user account available for testing (or multi-user environment)
- MCP tools configured
- User has access to Analytics > Tools tab

## Test Data

| Field | Value |
|-------|-------|
| User 1 | Current test user |
| User 2 | Secondary test user |
| Tool | list_files |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Analytics > Tools tab as User 1 | Note list_files CALLS and USERS |
| 2 | Execute agent that calls list_files (as User 1) | Tool executes |
| 3 | Execute same agent again (as User 1) | Tool executes again |
| 4 | Navigate to Analytics > Tools tab | CALLS +2, USERS = 1 (same user) |
| 5 | Log in as User 2 | Different user session |
| 6 | Execute agent that calls list_files (as User 2) | Tool executes |
| 7 | Navigate to Analytics > Tools tab | CALLS +1, USERS +1 (new unique user) |

## Expected Final State

USERS column shows unique user count. Multiple calls by same user don't inflate USERS. Different users are counted separately.

## Pass/Fail Criteria

**Pass:**
- USERS counts unique users only
- Same user multiple calls = 1 user
- USERS ≤ CALLS always

**Fail:**
- USERS counts total calls instead of unique users
- User not tracked
