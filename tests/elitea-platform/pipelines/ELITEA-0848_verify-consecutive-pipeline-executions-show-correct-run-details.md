---
id: ELITEA-0848
title: "Verify consecutive pipeline executions show correct run details"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines]
requirements: []
---
# ELITEA-0848: Verify consecutive pipeline executions show correct run details

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** When running a pipeline chat multiple times consecutively, the run details for non-first requests show as "completed" with empty results. This test verifies that each consecutive pipeline execution produces proper run details with complete results.

## Preconditions

User logged into Elitea stage.elitea.ai
A pipeline with at least one LLM node connected to END exists and is saved
Pipeline is functional (first execution completes successfully)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the pipeline detail page and locate the embedded chat panel on the right side | Pipeline detail page loads with embedded chat panel visible |
| 2 | Send a first message in the pipeline chat (e.g., 'Hello, test run 1') | Pipeline executes successfully. AI response appears in the chat. Run details show execution status with non-empty results |
| 3 | Open the run details/execution log for the first run by clicking on the run indicator | Run details panel shows the execution trace with node-by-node results. All node outputs are populated and status is 'completed' with actual data |
| 4 | Close the run details and send a second message in the pipeline chat (e.g., 'Hello, test run 2') | Pipeline executes the second request. AI response appears in the chat |
| 5 | Open the run details for the second execution | Run details show COMPLETE execution trace for the second run. Node outputs are populated (NOT empty). Status reflects actual execution, not just 'completed' with no data |
| 6 | Send a third message (e.g., 'Hello, test run 3') and check its run details | Third execution run details are fully populated with node-by-node results, matching the actual execution output |
| 7 | Compare the run details of all three executions | Each run has its own distinct, complete execution trace. No run shows empty results. Each run's output corresponds to its respective input message |
| 8 | Check the execution timestamps for each run in the run details — verify they are distinct and in chronological order | Each run has a unique timestamp that is later than the previous run. No timestamp duplication or out-of-order entries |
| 9 | Send a 4th message that intentionally causes a node error (e.g., invalid input for a Code node), then immediately send a 5th valid message | Run 4 shows an error state with meaningful error details in the run log. Run 5 shows a successful execution with complete results — the error in run 4 does not corrupt or affect run 5's details |
| 10 | Navigate away from the pipeline detail page (e.g., to Pipelines list), then return to the same pipeline and review the run history | All 5 run details are still accessible and correctly populated after page navigation — run history persists and is not lost on page re-entry |
| 11 | Refresh the browser page (F5) while on the pipeline detail page and verify run details are still accessible | Run history survives page refresh. All previous run details are accessible with correct execution traces and results intact |

## Expected Final State

Run history survives page refresh. All previous run details are accessible with correct execution traces and results intact

## Pass/Fail Criteria

PASS: Every consecutive pipeline execution shows complete run details with populated node outputs and accurate status; timestamps are distinct and chronological; error runs show proper error details without corrupting subsequent runs; run history persists across navigation and refresh
FAIL: Any non-first execution shows 'completed' status with empty results, run details are missing node output data, error in one run corrupts another's details, or run history is lost on navigation/refresh
