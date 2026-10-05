---
id: ELITEA-3680
title: "Budget — Private Project Budget Is Independent of Team Project Budget"
priority: medium
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, budget, private-project, team-project, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6573]
---
# ELITEA-3680: Budget — Private Project Budget Is Independent of Team Project Budget

**Module:** Analytics · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a user's Private project budget/usage total is completely independent of any Team project's budget — spending in one does not affect the other's spend, limit, or percent-used.

**Coverage:**
- Spending in a Team project does not change a Private project's budget/percent-used
- Spending in a Private project does not change a Team project's budget/percent-used

## Preconditions

- Access to a Private project and a Team project, both with a budget/limit configured, accessible by the same user

## Test Data

| Field | Value |
|-------|-------|
| Chat message | "Hello" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Private project's Usage/Budget page. Note spend and percent-used (baseline PB) | Baseline recorded |
| 2 | Navigate to the Team project's Usage/Budget page. Note spend and percent-used (baseline TB) | Baseline recorded |
| 3 | Send the test chat message in the Team project | LLM responds |
| 4 | Check the Team project's Usage/Budget page | Spend/percent-used increased from TB |
| 5 | Check the Private project's Usage/Budget page | Spend/percent-used is unchanged from PB |
| 6 | Send the test chat message in the Private project | LLM responds |
| 7 | Check the Private project's Usage/Budget page | Spend/percent-used increased from its step-5 value |
| 8 | Check the Team project's Usage/Budget page | Spend/percent-used is unchanged from step 4 |

## Expected Final State

Each project's budget page tracks only its own spend, completely independent of the other.

## Pass/Fail Criteria

**Pass:**
- Each project's budget/percent-used reflects only its own usage throughout

**Fail:**
- Spend in one project changes the other project's spend or percent-used
