---
id: ELITEA-4058
title: "Run detail total tokens add up to the agent and project totals"
priority: high
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, tokens, run-detail, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6998"]
---

# ELITEA-4058: Run detail total tokens add up to the agent and project totals

**Module:** analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that the per-run total tokens use the same rule as the aggregate endpoints, so the runs of an agent add up to its total, including cache tokens.

---

## Preconditions

- An agent run several times in a known time window on a model with prompt caching (e.g. a Claude-family model).

---

## Test Data

| Field | Value |
|-------|-------|
| Window | From just before the first run to after the last run |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | For each run, read `kpis.total_tokens` from `analytics_run_detail`. | A value per run. |
| 2 | Check each LLM call has `billable_input_tokens`. | Present. |
| 3 | Check each run total = sum over calls of billable input + output + cache read + cache write. | Equal for every run. |
| 4 | Sum the run totals. | A window total. |
| 5 | Compare with `total_tokens` from `analytics_agent_detail?entity_id=<agent>` and the agents list for the window. | Equal. |

---

## Expected Final State

Token totals agree between the run view and the agent/project views.

---

## Pass/Fail Criteria

**Pass:**
- Run totals use the same rule and add up exactly to the agent total.

**Fail:**
- Run totals exclude cache tokens or do not add up to the agent total.
