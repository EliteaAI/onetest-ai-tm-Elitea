---
id: ELITEA-1357
title: "Multiple HITL Nodes: Sequential Execution Through All HITL Pauses in a Single Run"
priority: high
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1357: Multiple HITL Nodes: Sequential Execution Through All HITL Pauses in a Single Run

**Module:** Pipeline Nodes · **Priority:** High · **Type:** Functional

**Objective:** Verify that a pipeline containing multiple sequential HITL nodes correctly pauses at each HITL node in order and captures independent decisions for each.

**Coverage:**
- First HITL node pauses and captures decision
- Pipeline progresses to second HITL node
- Second HITL node pauses and captures independent decision
- Both decisions recorded in Run Details

## Preconditions

- Pipeline: Node A → HITL1 → ... → HITL2 → End (two HITL nodes in sequence)
- Each HITL has a distinct USER MESSAGE to identify which pause is active
- Pipeline runnable in Chat interface

## Test Data

HITL1 USER MESSAGE: First review checkpoint; HITL2 USER MESSAGE: Second review checkpoint

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Run the pipeline in Chat interface | Pipeline reaches HITL1 and pauses; USER MESSAGE = 'First review checkpoint' |
| 2 | Click Approve on HITL1 | Pipeline continues past HITL1; progresses toward HITL2 |
| 3 | Pipeline reaches HITL2 | HITL2 pauses; USER MESSAGE = 'Second review checkpoint'; fresh action buttons appear |
| 4 | Click Reject on HITL2 | Pipeline continues along HITL2's Reject route; pipeline completes |
| 5 | Open Run Details | Both HITL1 (Approve) and HITL2 (Reject) decisions are recorded as separate entries |

## Expected Final State

Both HITL1 (Approve) and HITL2 (Reject) decisions are recorded as separate entries

## Pass/Fail Criteria

**Pass:**
- Both HITL nodes pause and resume correctly in order
- Independent decisions captured for each

**Fail:**
- Second HITL pause never triggers
- State from HITL1 corrupts HITL2
- Only one pause occurs in the run
