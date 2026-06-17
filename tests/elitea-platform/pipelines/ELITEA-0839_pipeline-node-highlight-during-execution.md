---
id: ELITEA-0839
title: "Pipeline Node Highlight During Execution"
priority: low
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [execution-highlighting, R-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3646, ProjectAlita/projectalita.github.io#3618]
---
# ELITEA-0839: Pipeline Node Highlight During Execution

**Module:** Pipelines · **Priority:** Low · **Type:** Functional

**Objective:** Verify that the currently executing node is visually highlighted in the editor/runtime UI during pipeline execution.

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
| 1 | Create a simple sequential pipeline (e.g., LLM → Target Node → END). | Pipeline is created and saved successfully. |
| 2 | Start pipeline execution. | The target node becomes visually highlighted when it starts executing. |
| 3 | Execution proceed to the next node | Highlight is removed from the previous node and applied only to the currently active node. At no time should multiple nodes appear highlighted as active |

## Expected Final State

Highlight is removed from the previous node and applied only to the currently active node. At no time should multiple nodes appear highlighted as active

## Pass/Fail Criteria

Pass Criteria
- Active node is highlighted during execution.
- Highlight appears consistently for each supported node type.
- Only one node is highlighted at a time.
