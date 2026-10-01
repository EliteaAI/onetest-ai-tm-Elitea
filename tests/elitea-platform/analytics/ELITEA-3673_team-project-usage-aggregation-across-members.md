---
id: ELITEA-3673
title: "Analytics — Team Project Usage Aggregation Across Members"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, team-project, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566]
---
# ELITEA-3673: Analytics — Team Project Usage Aggregation Across Members

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that when different members of the same team project send messages, the team project's Analytics totals reflect everyone's usage, not just whichever member is currently viewing the page.

**Coverage:**
- Team project LLM CALLS total aggregates calls from more than one member
- The total is correct regardless of which member is viewing the page

## Preconditions

- Access to a team project with at least 2 members

## Test Data

| Field | Value |
|-------|-------|
| Member 1 message | "What is 10% of 250?" |
| Member 2 message | "What is the capital of France?" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the team project's Analytics > Overview. Note LLM CALLS | Baseline recorded (N) |
| 2 | As Member 1, send their test message in the team project | LLM responds |
| 3 | As Member 2, send their test message in the same team project | LLM responds |
| 4 | Navigate to the team project's Analytics > Overview (as either member) | LLM CALLS = N + 2 — both members' calls are reflected in the shared project total |

## Expected Final State

The team project's total reflects every member's usage, regardless of who is viewing the Analytics page.

## Pass/Fail Criteria

**Pass:**
- Project total increases by both members' calls

**Fail:**
- Only one member's call is reflected in the project total
