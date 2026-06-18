---
id: ELITEA-0821
title: "Agent Node with Invalid input_mapping Data Type Surfaces an Error"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [rca:missing-functionality, feat:pipeline_nodes, feat:pipelines, r-2.0.1, eng:qa]
requirements: [ProjectAlita/projectalita.github.io#3742]
---
# ELITEA-0821: Agent Node with Invalid input_mapping Data Type Surfaces an Error

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that an Agent Node configured with an incompatible data type for `task` or `chat_history` in `input_mapping` surfaces a visible error rather than silently skipping or producing incorrect results.

**Coverage:**
- `task` field mapped to a pipeline state variable that holds a list type (array) instead of a string
- `chat_history` field set to a plain text string (Fixed type) instead of a list/array
- Error is surfaced in run output and Run Details popup for both variants
- Pipeline does not complete successfully with a type-mismatched input

## Preconditions

- Logged in at {{base_url}}
- Private project with pipeline creation rights
- At least one Agent configured in the project Toolkits
- A pipeline state variable of list type exists (e.g. a state variable named `items` with value `[\"a\", \"b\", \"c\"]`) — create one if not present

## Test Data

**Variant A — task type mismatch:**
- Task field: Type = Variable, Value = state variable holding a list (e.g. `items = [\"a\", \"b\", \"c\"]`)
- chat_history field: Type = Fixed, Value = `[]`

**Variant B — chat_history type mismatch:**
- Task field: Type = Fixed, Value = `Process input`
- chat_history field: Type = Fixed, Value = `Hello` (plain string instead of list)

Pipeline name: TC-AgentTypeValidation

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create pipeline 'TC-AgentTypeValidation'. Add Agent Node → End. Assign a valid Agent. | Agent Node added and connected to End. Agent is assigned. |
| 2 | **Variant A:** In the Agent Node config panel, set the Task field Type to 'Variable' and select a state variable that holds a list/array value (e.g. `items = ["a", "b", "c"]`). Set chat_history to a valid list value. Save. | Pipeline saved. Task is mapped to a list-typed variable. |
| 3 | Run the pipeline by sending a message. | Pipeline execution starts. |
| 4 | Observe the run output and chat area for error messages. | An error or validation message is displayed indicating the type mismatch. Run does not show success. |
| 5 | Open Run Details popup and inspect the error content. | Error section references the Task field type incompatibility. |
| 6 | **Variant B:** Edit the pipeline. Set the Task field to a valid string value. Set the chat_history field Type to 'Fixed' and enter a plain text string value (e.g. `Hello`) instead of a JSON array. Save. | Pipeline saved. chat_history is set to a plain string. |
| 7 | Run the pipeline by sending a message. | Pipeline execution starts. |
| 8 | Observe the run output and chat area for error messages. | An error or validation message is displayed indicating the type mismatch on chat_history. Run does not show success. |
| 9 | Open Run Details popup and inspect the error content. | Error section references the chat_history field type incompatibility. |

## Expected Final State

Error section references the chat_history field type incompatibility.

## Pass/Fail Criteria

**Pass:**
- An error or validation message is displayed for both variants
- Pipeline does not complete with a success status for either variant
- Run Details popup contains error details

**Fail:**
- Pipeline silently skips the Agent Node or completes with success for either variant
- No error message is shown despite the type mismatch
