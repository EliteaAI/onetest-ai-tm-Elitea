---
id: ELITEA-3674
title: "Analytics — Team Project Cost by User Attribution"
priority: medium
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, team-project, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566]
---
# ELITEA-3674: Analytics — Team Project Cost by User Attribution

**Module:** Analytics · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that within a team project, the "Cost by User" (or Users tab) breakdown attributes each member's calls to that specific member, not to a shared/generic row or to the project owner.

**Coverage:**
- Cost by User shows each member as a distinct row
- Each row reflects only that member's own calls

## Preconditions

- Access to a team project with at least 2 distinct members

## Test Data

| Field | Value |
|-------|-------|
| Member A message | "Define recursion" |
| Member B message | "Define polymorphism" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Member A, send the test message in the team project | LLM responds |
| 2 | As Member B, send their test message in the same team project | LLM responds |
| 3 | Navigate to the team project's Analytics > "Cost by User" (or Users) table | Both Member A and Member B appear as separate rows |
| 4 | Verify Member A's row only reflects Member A's call, and Member B's row only reflects Member B's | No overlap between the two rows |

## Expected Final State

Each member's usage is attributed to that specific member in the per-user breakdown.

## Pass/Fail Criteria

**Pass:**
- Each member's row shows only their own call

**Fail:**
- Both calls appear under one row, or either call is attributed to the wrong member
