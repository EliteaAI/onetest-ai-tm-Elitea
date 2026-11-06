---
id: ELITEA-4392
title: "Models table attributes multi-model runs correctly: RUNS per model, LLM CALLS counted separately"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, issue:7033, r-2.0.8, agent-pipeline-analytics, models, multi-model]
requirements: [EliteaAI/elitea_issues#7033]
---

# ELITEA-4392: Models table attributes multi-model runs correctly: RUNS per model, LLM CALLS counted separately

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Models table reflects actual LLM execution records (not the Agent/Pipeline's configured default model), that a run using N models is counted once in each of those N models' RUNS rows, that LLM CALLS reflects the true call count (including repeated calls to the same model within a run), and that the Models table's RUNS column summed across rows may legitimately exceed total run count without being treated as a defect.

**Coverage:**
- Models table reflects actual execution records, not configured default model
- A multi-model run increments RUNS for every model it used
- A model called multiple times within one run: RUNS counted once per run, LLM CALLS reflects actual call count
- Sum of RUNS across Models rows may exceed total run count by design
- "Unknown model" fallback for missing model attribution
- Default sort TOTAL TOKENS descending

## Preconditions

- Logged in to `{{base_url}}`
- An Agent or Pipeline with at least one historical run that invoked more than one LLM model within a single run (multi-model run) is available
- Within that multi-model run, at least one model was called more than once (if available) to validate the RUNS-vs-LLM-CALLS distinction

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Entity | Agent or Pipeline with a known multi-model run |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the detail view for the test Agent/Pipeline and locate the Models table | Table renders with MODEL, RUNS, LLM CALLS, TOTAL TOKENS, COST columns |
| 2 | Identify the known multi-model run and check that each model it used shows up as its own row | Every model actually invoked by that run appears as a distinct row; none of the invoked models is missing |
| 3 | Confirm that run's RUNS count is incremented in EVERY model row it used, not only one | Each applicable model row's RUNS includes +1 for this run |
| 4 | For a model called multiple times within that one run, compare RUNS vs LLM CALLS for that model | RUNS for the run is counted once; LLM CALLS reflects the actual number of calls (greater than 1) |
| 5 | Sum the RUNS column across all Models rows and compare to the total run count shown elsewhere on the page (e.g. KPI card) | Models RUNS sum may legitimately exceed total run count; this is not flagged as a defect |
| 6 | Check the Models table for any usage record known to lack model attribution (if available in test data) | Such records appear grouped under "Unknown model" rather than omitted |
| 7 | Confirm the Models table is not simply listing the Agent/Pipeline's configured default model when that model was not actually invoked | Only models with actual execution records appear |
| 8 | Observe the table's default sort order on initial load | Rows are sorted by TOTAL TOKENS descending by default |

## Expected Final State

The Models table shows one row per model actually invoked, with every multi-model run counted in all applicable model rows, LLM CALLS independently tracking actual call volume, and the table defaulting to TOTAL TOKENS descending sort.

## Pass/Fail Criteria

**Pass:**
- Multi-model runs increment RUNS in every model row they used
- LLM CALLS for a repeatedly-called model exceeds its RUNS contribution for that run, reflecting true call count
- Sum of RUNS across the table may exceed total run count without being a defect
- "Unknown model" used for unattributed usage records
- Default sort is TOTAL TOKENS descending

**Fail:**
- A multi-model run is only attributed to one model
- LLM CALLS equals RUNS when a model was called multiple times within a run
- The table shows the Agent/Pipeline's configured default model instead of actual execution records
- Default sort is not TOTAL TOKENS descending
