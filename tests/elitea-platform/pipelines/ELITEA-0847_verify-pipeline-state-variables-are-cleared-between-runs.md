---
id: ELITEA-0847
title: "Verify pipeline state variables are cleared between runs"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines]
requirements: []
---
# ELITEA-0847: Verify pipeline state variables are cleared between runs

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Pipeline state variables persist between runs instead of being reset. This causes stale data from previous executions to leak into subsequent runs, producing incorrect results. This test verifies that state is properly reset between pipeline executions.

## Preconditions

User logged into Elitea stage.elitea.ai
A pipeline exists with State modifier nodes that set and read state variables
Pipeline has at least: an input node, a State modifier node that writes a state variable, an LLM or Code node that reads the state, and an END node

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the pipeline detail page that uses state variables | Pipeline detail page loads with the flow editor showing nodes including State modifier |
| 2 | Open the pipeline YAML editor and verify the state variable definitions and their default values | YAML shows state variable definitions with initial/default values (e.g., empty string, empty array, or zero) |
| 3 | Switch back to Flow view. Send a first message in the embedded chat that triggers state modification (e.g., a message that causes the pipeline to store a value in state) | Pipeline executes. The state variable is populated with data from the first run. Response reflects the state value |
| 4 | Examine the run details of the first execution to confirm the state variable was set | Run details show the state variable was written with the expected value from the first run |
| 5 | Send a second message that reads the state variable without explicitly setting new values | The second run should start with CLEAN/DEFAULT state values, not carry over values from the first run. Response should reflect default or empty state, not previous run's data |
| 6 | Examine the run details of the second execution to verify state was reset | State variables at the beginning of the second run show default values, not values from the first run |
| 7 | Clear the chat history and run the pipeline again with a new message | After clearing chat, the pipeline state is completely fresh. State variables start at their default values |
| 8 | Compare state variable values across all three runs at their initial node execution point | Each run starts with default/clean state values. No cross-run state pollution occurs |

## Expected Final State

Each run starts with default/clean state values. No cross-run state pollution occurs

## Pass/Fail Criteria

PASS: Each pipeline run starts with default state values; no stale data from previous runs affects subsequent executions
FAIL: State variables from a previous run persist into the next run, causing stale or incorrect data in subsequent executions
