---
id: ELITEA-4060
title: "Analytics aggregate views equal the sum of the runs in the window"
priority: high
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, aggregates, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6566"]
---

# ELITEA-4060: Analytics aggregate views equal the sum of the runs in the window

**Module:** analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Costs, Agents, Tools, Users and Usage views for a time window equal the sum of the individual runs made in that window.

---

## Preconditions

- A quiet project (or a narrow window) so that only test runs fall in it.
- An agent with tools and a pipeline, run several times on two or more models.

---

## Test Data

| Field | Value |
|-------|-------|
| Window | Covering only the test runs |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Collect every run's detail (LLM calls, tool calls, tokens, cost) for the window. | Sums per model, tool, user and agent computed. |
| 2 | Costs → by model: compare calls, input, output and cost per model. | Equal to the sums. |
| 3 | Agents list and agent detail: compare events, tool counts and cost. | Equal. |
| 4 | Tools list: compare calls per tool. | Equal. |
| 5 | Users list: compare LLM and tool events per user. | Equal. |
| 6 | Usage KPIs: compare LLM calls and the models list. | LLM calls equal; every model used is listed. |
| 7 | Activity: check active and AI-active users. | Equal to the number of users who ran tests. |

---

## Expected Final State

Every aggregate is consistent with the individual runs.

---

## Pass/Fail Criteria

**Pass:**
- All aggregates equal the sums of the runs.

**Fail:**
- Any aggregate differs from the sum of its runs.
