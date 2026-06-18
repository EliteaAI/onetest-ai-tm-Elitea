---
id: ELITEA-1353
title: "Run Details: HITL Node State Before and After Decision Displayed Correctly"
priority: high
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1353: Run Details: HITL Node State Before and After Decision Displayed Correctly

**Module:** Pipeline Nodes · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Run Details panel for a completed pipeline run shows the HITL node's Before and After state correctly, including the reviewer's decision.

**Coverage:**
- HITL node appears as a step in Run Details
- Before state (at pause) is correctly recorded
- After state (post-decision, including reviewer action) is correctly recorded
- Reviewer decision action visible in the record

## Preconditions

- A pipeline with HITL node has been run and a decision has been submitted (any route)
- Run Details / execution log panel is accessible from the pipeline or chat view

## Test Data

Completed pipeline run that included HITL Approve decision; Known pipeline state values at the time of pause

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Run Details / pipeline execution log for the completed HITL run | Run Details panel shows per-node execution entries |
| 2 | Locate the HITL node entry in the run log | HITL node is listed as a step in the execution sequence |
| 3 | Expand the HITL node step and view its Before state | Before state shows the pipeline state at pause time (input data, upstream values) |
| 4 | View the After state | After state shows updated pipeline state including reviewer's decision (e.g., approved) and any edit feedback |
| 5 | Confirm the reviewer action is recorded (Approve/Edit/Reject) | Decision label is visible in the HITL node run entry |

## Expected Final State

Decision label is visible in the HITL node run entry

## Pass/Fail Criteria

**Pass:**
- Both Before and After states are present and accurate
- Reviewer decision is recorded and visible

**Fail:**
- HITL node absent from Run Details
- Before or After state not shown
- Decision action not recorded
