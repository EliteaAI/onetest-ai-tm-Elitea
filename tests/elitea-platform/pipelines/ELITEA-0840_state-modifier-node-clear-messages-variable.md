---
id: ELITEA-0840
title: "State Modifier Node - Clear Messages Variable"
priority: high
type: functional
module: pipelines
status: draft
execution_type: automated
tags: [state-modifier, pipeline, backend]
requirements: []
---
# ELITEA-0840: State Modifier Node - Clear Messages Variable

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that State Modifier node correctly clears the `messages` variable when 'Clear' operation is selected, and subsequent nodes receive empty message history.

## Preconditions

- User logged in to Elitea stage environment
- User has permissions to create and execute pipelines
- Understanding of State Modifier node operations

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new pipeline named 'State Modifier Messages Clear Test' | Pipeline created successfully |
| 2 | Add an LLM node (Node A) and configure it to process a test message | Node A added to canvas, configured to populate `messages` variable |
| 3 | Add a State Modifier node after Node A | State Modifier node added and connected to Node A |
| 4 | Configure State Modifier node: select variable `messages`, set operation to 'Clear' | State Modifier configured with Clear operation on `messages` variable |
| 5 | Add another LLM node (Node B) after State Modifier node | Node B added and connected to State Modifier |
| 6 | Execute the pipeline with input: 'Test message' | Pipeline execution starts, Node A processes message |
| 7 | Inspect pipeline execution logs/state after State Modifier node | State Modifier execution shows `messages` variable cleared (empty array [] or removed) |
| 8 | Verify Node B execution logs | Node B starts with empty message history, no messages from Node A visible |

## Expected Final State

Node B starts with empty message history, no messages from Node A visible

## Pass/Fail Criteria

PASS: After State Modifier execution, `messages` variable is empty array [] or removed from state, Node B receives no messages from Node A
FAIL: State Modifier does not clear `messages`, Node B still sees messages from Node A
