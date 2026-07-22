---
id: ELITEA-2311
title: "Overview tab displays all six KPI cards with correct labels and non-empty values"
priority: medium
type: functional
module: settings-analytics
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2311: Overview tab displays all six KPI cards with correct labels and non-empty values

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Overview tab displays all six KPI cards with correct labels and non-empty values. Success is confirmed when verify none of the cards show "undefined", "nan", or blank values.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Analytics → Overview tab | Target page/section loads successfully. |
| 2 | Verify the following 6 KPI cards are shown with correct labels and subtitles: | Condition holds as described. |
| 3 | TEAM — "X of Y active members" | Action completes without error and produces the expected UI state. |
| 4 | AI ACTIVE — value + adoption percentage in green + "% adoption" subtitle | Action completes without error and produces the expected UI state. |
| 5 | LLM CALLS — numeric value + "event_type = llm" subtitle | Action completes without error and produces the expected UI state. |
| 6 | TOOL RUNS — numeric value + "event_type = tool" subtitle | Action completes without error and produces the expected UI state. |
| 7 | CHAT MSG — numeric value + "user messages sent" subtitle | Action completes without error and produces the expected UI state. |
| 8 | AGENT RUNS — numeric value + "agents and pipelines interactions" subtitle | Action completes without error and produces the expected UI state. |
| 9 | Verify none of the cards show "undefined", "NaN", or blank values | Condition holds as described. |

---

## Expected Final State

Verify none of the cards show "undefined", "NaN", or blank values.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Overview tab displays all six KPI cards with correct labels and non-empty values.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
