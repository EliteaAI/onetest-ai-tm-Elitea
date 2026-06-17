---
id: ELITEA-0887
title: "Chat Message Trigger — Execution and Run History"
priority: high
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [regression, pipeline, R-2.0.3, trigger, smoke]
requirements: [EliteaAI/elitea_issues#4827]
---
# ELITEA-0887: Chat Message Trigger — Execution and Run History

**Module:** Entrypoint Trigger Type · **Priority:** High · **Type:** Functional

**Objective:** Verifies that a pipeline configured with the Chat Message trigger executes successfully when a message is sent, that no additional config fields appear for this trigger type, and that no trigger label/notification appears in run history for Chat Message runs.

## Preconditions

User is logged in
A pipeline with Chat Message trigger configured on the Entrypoint node exists and is in a ready/published state
The pipeline is accessible from a conversation or the pipeline execution view

## Test Data

Pipeline: Chat Message trigger, at least one processing node, produces observable output
Test input message: "Hello, pipeline test"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline in edit mode and select the Entrypoint node | Node config panel opens |
| 2 | Set the Trigger dropdown to 'Chat Message' (or confirm it is already set) | No additional configuration fields appear below the Trigger dropdown |
| 3 | Trigger the pipeline by sending a chat message (e.g., via a conversation that uses this pipeline) | Pipeline begins execution |
| 4 | Wait for pipeline execution to complete | Pipeline executes successfully end-to-end and produces the expected output |
| 5 | Navigate to the pipeline's run history | Run history is displayed |
| 6 | Locate the run just triggered | The run entry in run history has no trigger source label or notification — it appears as a plain run with no special badge |

## Expected Final State

The run entry in run history has no trigger source label or notification — it appears as a plain run with no special badge

## Pass/Fail Criteria

PASS: Execution completes successfully; no config fields for Chat Message; no trigger notification in run history
FAIL: Execution fails; extra config fields appear for Chat Message; a trigger label/badge appears in run history for a Chat Message run
