---
id: ELITEA-2586
title: "Trace steps are ordered by started_at timestamp"
priority: medium
type: functional
module: trace-steps-api
status: ready
execution_type: manual
tags: [nfr:performance, eng:backend, epic:5724]
requirements: [EliteaAI/elitea_issues#5724, EliteaAI/elitea_issues#5727]
---
# ELITEA-2586: Trace steps are ordered by started_at timestamp

**Module:** Trace Steps API · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that trace steps are returned ordered by `(started_at, id)` to maintain correct execution order.

**Coverage:**
- Steps are ordered chronologically by started_at
- When started_at is identical, id is used as tiebreaker
- Order matches actual execution sequence

## Preconditions

- Logged in to {{base_url}}
- Access to a conversation with multiple sequential tool calls
- API testing tool available

## Test Data

| Field | Value |
|-------|-------|
| Agent | Agent that executes multiple tools in sequence |
| Expected order | Matches execution order in conversation |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create conversation where agent executes 5+ tools in sequence | Tools execute in known order |
| 2 | Call trace steps endpoint for this message group | Returns all tool calls |
| 3 | Verify started_at timestamps are in ascending order | Each step's started_at >= previous step's started_at |
| 4 | Compare order with UI display order | API order matches what UI shows |
| 5 | Verify order matches actual execution sequence | First tool executed appears first in response |

## Expected Final State

Trace steps are returned in chronological execution order, matching both the UI display and the actual execution sequence.

## Pass/Fail Criteria

**Pass:**
- started_at values are in ascending order
- Order matches execution sequence
- Order matches UI display

**Fail:**
- Steps returned in wrong order
- Timestamps not ascending
- Order doesn't match UI/execution sequence
