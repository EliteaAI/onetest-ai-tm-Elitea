---
id: ELITEA-0838
title: "Last Executed Node Highlight During Interruption"
priority: low
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [interrupted-state-highlighting, R-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3646]
---
# ELITEA-0838: Last Executed Node Highlight During Interruption

**Module:** Pipelines · **Priority:** Low · **Type:** Functional

**Objective:** Verify that when execution is interrupted, the last executed node remains highlighted until execution resumes, for each supported node type.

## Preconditions

- User is logged in
- Execution can be started successfully
- Target node type under test is available in the system

## Test Data

Supported node types to validate individually:

- Agent
- Mcp
- Code
- Printer
- State Modifier
- LLM
- Toolkit
- Custom

Additionally
- Router
- Decision

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a simple sequential pipeline containing the target node type. | Pipeline is saved successfully |
| 2 | Start pipeline execution. | Target node becomes highlighted when execution reaches it. |
| 3 | Trigger interruption while the target node is active. | Execution pauses. |
| 4 | Observe Flow view. | The last executed node remains highlighted. No other nodes are highlighted. |
| 5 | Resume execution. | Highlight transitions to the next active node according to execution flow. |

## Expected Final State

Highlight transitions to the next active node according to execution flow.

## Pass/Fail Criteria

Pass Criteria
- Highlight remains visible during interruption.
- Highlight updates correctly after resume.
- Behavior is consistent across all supported node types.
