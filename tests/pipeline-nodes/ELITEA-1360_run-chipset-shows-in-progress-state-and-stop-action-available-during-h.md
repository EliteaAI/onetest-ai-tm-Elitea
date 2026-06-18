---
id: ELITEA-1360
title: "Run Chipset Shows In Progress State and Stop Action Available During HITL Pause"
priority: medium
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1360: Run Chipset Shows In Progress State and Stop Action Available During HITL Pause

**Module:** Pipeline Nodes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that while a pipeline is paused at a HITL node, the run chipset shows "In Progress" with a spinner and a "Stop" button is available.

**Coverage:**
- Run chipset state during HITL pause = "In Progress" with spinner
- Stop button available and enabled during pause

## Preconditions

- Pipeline with HITL node currently paused (waiting for human decision) in Chat interface

## Test Data

Active pipeline run in paused state

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | While pipeline is paused at HITL, locate the run chipset / run status indicator in the UI | Run chipset is visible (in pipeline run list or Chat header area) |
| 2 | Observe the run state indicator | Shows 'In Progress' state with a blue spinning indicator |
| 3 | Verify a Stop action button is available on the run chipset | Stop button is present and not disabled |
| 4 | Confirm Stop button is active/enabled | Button is clickable (visual confirmation only — do not click to avoid stopping the test run) |

## Expected Final State

Button is clickable (visual confirmation only — do not click to avoid stopping the test run)

## Pass/Fail Criteria

**Pass:**
- Run chipset shows 'In Progress' + active spinner during HITL pause
- Stop button visible and enabled

**Fail:**
- Run chipset shows wrong state (e.g., 'Completed' or 'Error') during pause
- Stop button absent or disabled
