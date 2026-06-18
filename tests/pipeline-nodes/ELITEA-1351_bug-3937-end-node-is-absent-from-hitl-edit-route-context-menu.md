---
id: ELITEA-1351
title: "Bug #3937: End Node Is Absent From HITL Edit Route Context Menu"
priority: high
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3937, ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1351: Bug #3937: End Node Is Absent From HITL Edit Route Context Menu

**Module:** Pipeline Nodes · **Priority:** High · **Type:** Functional

**Objective:** Verify that the End node is not available in the connection context menu when dragging from the HITL node's Edit route output handle (regression test for Bug #3937).

**Coverage:**
- Edit route context menu does not include the End node
- Other valid node types are still listed
- Approve and Reject route context menus not broken

## Preconditions

- Pipeline editor open with a HITL node on the canvas

## Test Data

N/A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | On the HITL node, locate the Edit output handle (middle route handle) | Edit handle is visible |
| 2 | Click and drag from the Edit output handle to an empty canvas area | A node-picker context menu appears for the Edit route |
| 3 | Inspect the list of available node types | The End node is NOT present in the context menu; only valid continuation nodes are listed |
| 4 | Repeat with the Approve and Reject handles to confirm they are unaffected | Context menus for Approve/Reject open without errors |

## Expected Final State

Context menus for Approve/Reject open without errors

## Pass/Fail Criteria

**Pass:**
- End node is absent from the Edit route context menu (bug #3937 is fixed)

**Fail:**
- End node appears as a selectable option when dragging from the Edit route handle (Bug #3937 regression)
