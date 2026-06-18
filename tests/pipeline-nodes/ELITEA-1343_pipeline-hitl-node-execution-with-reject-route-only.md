---
id: ELITEA-1343
title: "Pipeline HITL Node: Execution With Reject Route Only"
priority: critical
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1343: Pipeline HITL Node: Execution With Reject Route Only

**Module:** Pipeline Nodes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a pipeline with a HITL node where only the Reject route is connected handles the minimal-route configuration gracefully.

**Coverage:**
- HITL node with a single wired route (Reject only)
- Approve and Edit buttons absent or disabled
- Reject route execution

## Preconditions

- Pipeline with HITL node where only the Reject output handle is connected to a downstream node; Approve and Edit handles are unconnected
- Pipeline runnable in Chat interface

## Test Data

Pipeline input: any text message

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm in pipeline editor that only the Reject handle has a downstream connection | Approve and Edit handles are free; Reject handle is wired |
| 2 | In Chat interface, trigger the pipeline run | Pipeline pauses at HITL; USER MESSAGE displayed; action buttons shown |
| 3 | Inspect the available buttons | Only the Reject button is active; Approve and Edit are absent or disabled |
| 4 | Click Reject | Pipeline resumes via Reject route; downstream node executes; pipeline completes without errors |

## Expected Final State

Pipeline resumes via Reject route; downstream node executes; pipeline completes without errors

## Pass/Fail Criteria

**Pass:**
- HITL node functions with only one wired route
- Reject executes correctly
- No crash, hang, or unexpected error

**Fail:**
- Pipeline crashes with only one route wired
- Incorrect buttons shown
- Reject action fails to execute
