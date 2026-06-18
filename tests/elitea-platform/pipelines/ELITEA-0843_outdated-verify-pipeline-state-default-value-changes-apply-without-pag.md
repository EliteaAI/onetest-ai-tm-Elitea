---
id: ELITEA-0843
title: "[OUTDATED] Verify pipeline state default value changes apply without page reload"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, outdated]
requirements: []
---
# ELITEA-0843: [OUTDATED] Verify pipeline state default value changes apply without page reload

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Changing default values for pipeline state variables does not take effect until the page is reloaded or the chat is cleared. This test verifies that state default value changes are applied in real-time and reflected in subsequent pipeline executions without requiring a page reload.

## Preconditions

User logged into Elitea stage.elitea.ai
A pipeline exists with state variables that have configurable default values
The pipeline has a Code or LLM node that reads and outputs the state variable value

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the pipeline detail page with state variables configured | Pipeline editor loads showing the flow with State modifier nodes |
| 2 | Execute the pipeline by sending a message in the embedded chat. Note the initial state variable value in the response | Pipeline executes successfully. Response includes the current default value of the state variable (e.g., default string 'hello') |
| 3 | Without reloading the page, modify the default value of the state variable in the pipeline configuration (e.g., change from 'hello' to 'world') | State variable default value is updated in the configuration UI |
| 4 | Save the pipeline by clicking Save | Pipeline saves successfully |
| 5 | WITHOUT reloading the page or clearing chat, send another message in the embedded chat to trigger a new pipeline execution | Pipeline executes with the UPDATED default value. The response reflects the new default value 'world', not the old value 'hello' |
| 6 | Verify the run details show the updated default value was used at pipeline initialization | Run details confirm the state variable started with the new default value 'world' |
| 7 | Change the default value again (e.g., to 'test123'), save, and immediately execute without reload | Pipeline uses the latest default value 'test123' without requiring page reload or chat clearing |
| 8 | Compare all three execution results to confirm each used the correct default value at the time of execution | Run 1 used 'hello', Run 2 used 'world', Run 3 used 'test123'. Each execution correctly reflected the current default value |

## Expected Final State

Run 1 used 'hello', Run 2 used 'world', Run 3 used 'test123'. Each execution correctly reflected the current default value

## Pass/Fail Criteria

PASS: Updated default values are used in pipeline executions immediately after save without page reload
FAIL: Updated default values require page reload or chat clearing to take effect, or the old default values persist in subsequent runs after modification
