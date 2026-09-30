---
id: ELITEA-3427
title: "Tool Outcome Population Still Works Correctly After Reserving tool_outcomes/last_tool_outcome"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, state-variables, story:6593, reserved-variables, regression, tool-outcome]
requirements: [EliteaAI/elitea_issues#6593]
---
# ELITEA-3427: Tool Outcome Population Still Works After Reserving the System Variables

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm that reserving `tool_outcomes`/`last_tool_outcome` as system-managed names did not break the runtime population path (`FunctionTool._with_outcome()`, from #6164) that writes actual tool-call results into these variables during a pipeline run.

**Coverage:** Regression — the fix's PR description claims the population code path was untouched; this case verifies that rather than assuming it.

## Preconditions

- A pipeline exists with at least one tool node calling any configured toolkit
- User has permission to run the pipeline and view its run state

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Run the pipeline once, letting the tool node execute successfully. | Pipeline run completes. |
| 2 | Open the pipeline's run state view (raw JSON, e.g. via `PipelineStateViewModal`) and inspect `last_tool_outcome`. | Reflects the most recent tool call's outcome envelope (status, error_class, etc., per the #6164 envelope), not stale or missing. |
| 3 | Inspect `tool_outcomes` in the same run state. | Contains a per-node entry accumulated for the tool call made in step 1. |
| 4 | Cross-check the values from steps 2–3 against whatever the UI's read-only `tool_outcomes`/`last_tool_outcome` rows display for the same run (if visible per [[ELITEA-3423]]). | Values match between the raw run state and the UI row display. |
| 5 | Run the pipeline again with a tool node configured to fail (e.g. bad input). | `last_tool_outcome` reflects the failure (status/error_class matching the failure), and `tool_outcomes` still accumulates the entry rather than dropping it. |

## Expected Final State

Runtime population of both variables during a pipeline run is unaffected by the reservation/validation changes — values are accurate, current, and consistent between raw state and any UI display.

## Pass/Fail Criteria

**Pass:**
- Steps 2, 3, and 5 show accurate, current values matching the actual tool call outcome
- Step 4 shows no mismatch between raw state and UI display

**Fail:**
- Either variable is missing, stale, or mismatched against the UI for the same run — would indicate the reservation guard interfered with the population path it wasn't supposed to touch
