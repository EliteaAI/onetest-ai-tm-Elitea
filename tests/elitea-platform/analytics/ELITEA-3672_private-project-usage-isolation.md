---
id: ELITEA-3672
title: "Analytics — Private Project Usage Isolation"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, private-project, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566]
---
# ELITEA-3672: Analytics — Private Project Usage Isolation

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that usage from a chat message sent inside a Private project is reflected in that project's own Analytics only, and does not show up in a different project's Analytics.

**Coverage:**
- Private project's own Analytics correctly reflects a new call
- A different project's Analytics is unaffected by that call

## Preconditions

- Logged in to {{base_url}}
- Access to at least one Private project (Project A) and one other project (Project B — private or team)

## Test Data

| Field | Value |
|-------|-------|
| Chat message | "Summarize the benefits of unit testing" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Switch to Project A. Navigate to Analytics > Overview. Note LLM CALLS and TOTAL COST | Baseline recorded for Project A |
| 2 | Switch to Project B. Navigate to Analytics > Overview. Note LLM CALLS and TOTAL COST | Baseline recorded for Project B |
| 3 | Switch to Project A and send the test chat message | LLM responds |
| 4 | Navigate to Project A's Analytics > Overview | LLM CALLS and TOTAL COST increased by exactly this call |
| 5 | Switch to Project B and check its Analytics > Overview | LLM CALLS and TOTAL COST are unchanged from the step 2 baseline |

## Expected Final State

Only Project A's Analytics reflect the new call; Project B's numbers are untouched.

## Pass/Fail Criteria

**Pass:**
- Project A's numbers increase correctly
- Project B's numbers are completely unchanged

**Fail:**
- Project B's numbers change at all after a call made only in Project A
