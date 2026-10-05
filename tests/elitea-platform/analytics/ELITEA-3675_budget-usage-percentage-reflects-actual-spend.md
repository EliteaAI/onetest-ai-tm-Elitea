---
id: ELITEA-3675
title: "Analytics — Budget Usage Percentage Reflects Actual Spend"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, budget, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6573]
---
# ELITEA-3675: Analytics — Budget Usage Percentage Reflects Actual Spend

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that a project's budget/usage page shows the correct percent-used and remaining budget, and that the percentage updates after new usage is added.

**Coverage:**
- Percent-used increases correctly after new spend
- Percent-used matches spend/limit

## Preconditions

- Logged in to {{base_url}} with access to a project that has a monthly budget/limit configured
- Access to Settings > Usage (or the project's budget page)

## Test Data

| Field | Value |
|-------|-------|
| Chat message | "Hello" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the project's Usage/Budget page | Note current spend, limit, and percent-used (e.g., X%) |
| 2 | Send the test chat message in the project | LLM responds, cost is recorded |
| 3 | Navigate back to the Usage/Budget page | Spend has increased, and percent-used has increased accordingly |
| 4 | Verify percent-used = (current spend / limit) × 100, roughly matching what's displayed | Calculation is consistent with the displayed numbers |

## Expected Final State

The budget page's percent-used and remaining-budget figures stay accurate as new usage is added.

## Pass/Fail Criteria

**Pass:**
- Spend and percent-used both increase correctly after the call
- Percent-used matches spend/limit

**Fail:**
- Percent-used doesn't update after new spend, or doesn't match spend/limit
