---
id: ELITEA-4393
title: "Trigger Sources table assigns exactly one source per run and never defaults unattributed runs to Manual"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, issue:7033, r-2.0.8, agent-pipeline-analytics, trigger-sources]
requirements: [EliteaAI/elitea_issues#7033]
---

# ELITEA-4393: Trigger Sources table assigns exactly one source per run and never defaults unattributed runs to Manual

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Trigger Sources table attributes each run to exactly one recorded trigger source (e.g. manual/chat, API, schedule, or invocation by another Agent/Pipeline), that a run with missing trigger metadata is shown under "Unknown" rather than assumed to be manual, that downstream LLM/tool calls are never counted as additional triggers, and that the table defaults to RUNS descending sort.

**Coverage:**
- Each run attributed to exactly one trigger source, no double-counting across sources
- Runs with missing trigger metadata shown as "Unknown", never defaulted to "Manual"
- Downstream LLM/tool calls not counted as additional triggers
- Default sort RUNS descending

## Preconditions

- Logged in to `{{base_url}}`
- An Agent or Pipeline with runs triggered from at least 2 different sources (e.g. manual/chat and API, or schedule) is available
- At least one run with missing/legacy trigger metadata exists, if available in the test environment

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Entity | Agent or Pipeline with runs from ≥2 trigger sources |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the detail view for the test Agent/Pipeline and locate the Trigger Sources table | Table renders with TRIGGER, RUNS, TOTAL TOKENS, COST columns |
| 2 | Confirm each known trigger source (e.g. manual/chat, API, schedule) appears as its own row with correct RUNS/TOTAL TOKENS/COST | Each source has a distinct row; metrics look consistent with known test runs |
| 3 | Sum the RUNS column across all Trigger Sources rows and compare to the total run count for the period | Sum equals total run count — no run is double-counted across multiple trigger-source rows |
| 4 | If a run with missing/legacy trigger metadata is available, confirm it appears under "Unknown" | Row labeled "Unknown" is present and includes that run; it is NOT grouped under "Manual" |
| 5 | For a run known to make multiple downstream LLM or tool calls, confirm it is still counted as exactly one run under its one initiating trigger source | No extra trigger rows or inflated RUNS counts attributable to downstream calls |
| 6 | Observe the table's default sort order on initial load | Rows are sorted by RUNS descending by default |

## Expected Final State

The Trigger Sources table attributes every run to exactly one source, correctly isolates unattributed runs under "Unknown" (never "Manual"), excludes downstream calls from trigger counting, and defaults to RUNS descending sort.

## Pass/Fail Criteria

**Pass:**
- Sum of RUNS across Trigger Sources rows equals total run count (no double-counting)
- Runs with missing trigger metadata appear under "Unknown", never "Manual"
- Downstream LLM/tool calls are not counted as additional triggers
- Default sort is RUNS descending

**Fail:**
- A run appears in more than one trigger-source row, or RUNS sum exceeds total run count
- A run with missing trigger metadata is shown under "Manual" instead of "Unknown"
- Downstream calls inflate trigger counts
- Default sort is not RUNS descending
