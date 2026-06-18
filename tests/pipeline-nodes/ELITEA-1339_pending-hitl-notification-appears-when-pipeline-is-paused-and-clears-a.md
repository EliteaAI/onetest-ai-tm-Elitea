---
id: ELITEA-1339
title: "Pending HITL Notification: Appears When Pipeline Is Paused and Clears After Decision"
priority: high
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1339: Pending HITL Notification: Appears When Pipeline Is Paused and Clears After Decision

**Module:** Pipeline Nodes · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a pipeline is paused at a HITL node, a notification indicator appears to alert the reviewer, and clears automatically after the decision is made.

**Coverage:**
- Notification indicator appears on HITL pause
- Notification persists while no decision is made
- Notification clears after decision is submitted

## Preconditions

- Pipeline with HITL node running in Chat interface
- Reviewer logged in with review permissions

## Test Data

Active pipeline run reaching HITL pause

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Trigger pipeline run; wait for HITL pause | Pipeline pauses; a notification indicator (bell, badge, or alert) appears in the UI signaling a pending decision |
| 2 | Locate the notification and read its content | Notification indicates a pipeline is paused waiting for human decision; pipeline/run is identifiable |
| 3 | Do not make a decision; observe the notification | Notification remains active |
| 4 | Navigate to the HITL pause and click Approve | Decision made successfully |
| 5 | Check the notification indicator | Notification is cleared/dismissed; no lingering 'pending decision' indicator |

## Expected Final State

Notification is cleared/dismissed; no lingering 'pending decision' indicator

## Pass/Fail Criteria

**Pass:**
- Notification appears on pause, persists until decision, and clears after

**Fail:**
- No notification on pause
- Notification does not clear after decision
- Stale notification remains after decision
