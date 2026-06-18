---
id: ELITEA-1346
title: "State Persists at HITL Pause Across Browser Refresh"
priority: critical
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1346: State Persists at HITL Pause Across Browser Refresh

**Module:** Pipeline Nodes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a pipeline paused at a HITL node retains its paused state and action buttons after a browser refresh (LangGraph checkpointer persistence).

**Coverage:**
- HITL pause state survives browser refresh
- USER MESSAGE and action buttons re-appear after reload
- Pipeline resumes correctly from the persisted state

## Preconditions

- Pipeline with HITL node is running in Chat interface
- Pipeline has reached the HITL pause point (USER MESSAGE displayed, action buttons visible)

## Test Data

Active pipeline run URL

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Trigger pipeline run; wait for it to pause at the HITL node | Pipeline is paused; USER MESSAGE visible; Approve/Edit/Reject buttons shown |
| 2 | Note the current page URL | URL recorded |
| 3 | Refresh the browser (F5 / Ctrl+R) | Page reloads |
| 4 | Navigate back to the Chat interface or pipeline run view | Pipeline run is still in paused/waiting state; HITL USER MESSAGE is still displayed; action buttons are still available |
| 5 | Click Approve | Pipeline resumes correctly from the persisted paused state; downstream node executes; no data loss |

## Expected Final State

Pipeline resumes correctly from the persisted paused state; downstream node executes; no data loss

## Pass/Fail Criteria

**Pass:**
- HITL pause state survives browser refresh
- Action buttons remain available after reload
- Pipeline resumes correctly after decision post-refresh

**Fail:**
- State is lost on browser refresh
- Buttons disappear after reload
- Pipeline run transitions to error state after refresh
