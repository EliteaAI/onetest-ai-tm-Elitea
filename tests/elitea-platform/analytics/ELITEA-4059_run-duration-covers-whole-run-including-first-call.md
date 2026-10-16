---
id: ELITEA-4059
title: "Run duration covers the whole run, including the first LLM call"
priority: high
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, duration, run-detail, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6566"]
---

# ELITEA-4059: Run duration covers the whole run, including the first LLM call

**Module:** analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that a run's duration includes the first LLM call, so a run with a single call is never shown as 0 ms.

---

## Preconditions

- An agent; API access.

---

## Test Data

| Field | Value |
|-------|-------|
| Prompts | A plain question (single LLM call) and the tool prompt (several calls) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the plain prompt and note how long the predict request took. | Some seconds. |
| 2 | Read `duration_ms`, `started_at` and `ended_at` from `analytics_run_detail`, and the LLM call's own `duration_ms`. | Values available. |
| 3 | Check the run duration. | Not 0; at least the LLM call's duration; `started_at` is before `ended_at`. |
| 4 | Run the tool prompt and repeat. | Run duration ≥ the sum of the call durations, and not less than the first call alone. |

---

## Expected Final State

Run duration reflects the real time spent in the run.

---

## Pass/Fail Criteria

**Pass:**
- No run shows 0 ms; run duration includes the first event.

**Fail:**
- Single-call runs show 0 ms, or multi-call runs exclude the first call's time.
