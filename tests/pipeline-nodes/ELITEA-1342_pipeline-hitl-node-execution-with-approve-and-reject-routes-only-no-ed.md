---
id: ELITEA-1342
title: "Pipeline HITL Node: Execution With Approve and Reject Routes Only (No Edit)"
priority: critical
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1342: Pipeline HITL Node: Execution With Approve and Reject Routes Only (No Edit)

**Module:** Pipeline Nodes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a pipeline with a HITL node configured with only Approve and Reject routes (Edit route unconnected) executes without errors.

**Coverage:**
- HITL node with only two wired routes
- Absence or disabled state of the Edit action button
- Approve route execution
- Reject route execution

## Preconditions

- Pipeline with a HITL node where only Approve and Reject output handles are connected to downstream nodes; Edit handle is unconnected
- Pipeline runnable in Chat interface

## Test Data

Pipeline input: any text message

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline editor and confirm only Approve and Reject handles have connections; Edit handle is free | HITL node shows two wired routes; Edit handle has no connection |
| 2 | In Chat interface, trigger the pipeline run | Pipeline reaches HITL node and pauses; USER MESSAGE displayed; action buttons visible |
| 3 | Verify the available action buttons | At minimum Approve and Reject buttons are present; Edit button is either absent or disabled/greyed out |
| 4 | Click Approve | Pipeline resumes via Approve route; downstream node executes; no errors |
| 5 | Re-trigger the pipeline and click Reject | Pipeline resumes via Reject route; downstream node executes; no errors |

## Expected Final State

Pipeline resumes via Reject route; downstream node executes; no errors

## Pass/Fail Criteria

**Pass:**
- Pipeline executes correctly with only two active routes
- No crash or error when Edit route is unwired
- Approve and Reject both function correctly

**Fail:**
- Pipeline errors due to missing Edit connection
- Edit button enabled and clickable when route is not wired
- Pipeline fails to pause or fails to resume
