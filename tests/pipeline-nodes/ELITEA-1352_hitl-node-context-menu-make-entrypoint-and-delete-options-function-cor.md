---
id: ELITEA-1352
title: "HITL Node Context Menu: Make Entrypoint and Delete Options Function Correctly"
priority: high
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1352: HITL Node Context Menu: Make Entrypoint and Delete Options Function Correctly

**Module:** Pipeline Nodes · **Priority:** High · **Type:** Functional

**Objective:** Verify that the HITL node context menu provides functional "Make entrypoint" and "Delete" options, and that both operations work as expected.

**Coverage:**
- Context menu visibility and available options
- "Make entrypoint" designates HITL as entry point with visual indicator
- "Delete" removes the node from canvas cleanly

## Preconditions

- Pipeline editor open with a HITL node on canvas (not yet set as entry point)

## Test Data

N/A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Right-click (or use the three-dot menu) on the HITL node | Context menu appears with at minimum 'Make entrypoint' and 'Delete' options |
| 2 | Click Make entrypoint | HITL node is designated as the pipeline entry point; a visual indicator (e.g., 'Entry' badge) appears on the node; previous entry point loses designation |
| 3 | Right-click the HITL node again | Context menu now shows 'Remove entrypoint' (or equivalent) instead of 'Make entrypoint' |
| 4 | Add a second HITL node to the canvas; right-click it; click Delete | The new node is removed from the canvas cleanly; no errors; original HITL node unaffected |

## Expected Final State

The new node is removed from the canvas cleanly; no errors; original HITL node unaffected

## Pass/Fail Criteria

**Pass:**
- 'Make entrypoint' sets HITL as entry point with visible indicator
- 'Delete' removes the node without errors

**Fail:**
- Context menu missing required options
- 'Make entrypoint' has no visible effect
- 'Delete' does not remove the node or causes errors
