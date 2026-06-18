---
id: ELITEA-1341
title: "Pipeline HITL Node: Full Execution Through All Three Routes (Approve + Edit + Reject)"
priority: critical
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1341: Pipeline HITL Node: Full Execution Through All Three Routes (Approve + Edit + Reject)

**Module:** Pipeline Nodes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a pipeline with a HITL node correctly pauses for a human decision and resumes through all three configured routes.

**Coverage:**
- Pipeline execution pause at HITL node in Chat interface
- USER MESSAGE displayed to reviewer
- Approve route execution and downstream continuation
- Edit route execution and EDIT STATE KEY capture
- Reject route execution and downstream continuation

## Preconditions

- Logged in with pipeline edit and run permissions
- Pipeline configured with HITL node connected to three distinct downstream nodes (one per route)
- EDIT STATE KEY configured (e.g., reviewer_feedback)
- Pipeline published and runnable in the Chat interface (interactive mode)

## Test Data

Pipeline run input: any text message (e.g., "Run test"); Three downstream nodes labelled distinctly

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In the Chat interface, send a message to trigger the pipeline | Pipeline starts executing and reaches the HITL node; execution pauses |
| 2 | Observe the displayed USER MESSAGE and action buttons | USER MESSAGE text appears; Approve, Edit, and Reject buttons are all visible |
| 3 | Click Approve | Pipeline resumes via the Approve route; downstream Approve node executes; pipeline completes |
| 4 | Re-trigger the pipeline. When paused at HITL, click Edit | An edit input field appears; reviewer types feedback and submits; pipeline resumes via Edit route; EDIT STATE KEY captures the feedback |
| 5 | Re-trigger the pipeline. When paused at HITL, click Reject | Pipeline resumes via the Reject route; downstream Reject node executes; pipeline completes |

## Expected Final State

Pipeline resumes via the Reject route; downstream Reject node executes; pipeline completes

## Pass/Fail Criteria

**Pass:**
- All three routes execute correctly and route to their respective downstream nodes
- Edit route captures reviewer feedback in EDIT STATE KEY
- No errors on any route

**Fail:**
- Any route fails to execute or throws an error
- Pipeline gets stuck after a decision
- Wrong downstream node executed for a given action
