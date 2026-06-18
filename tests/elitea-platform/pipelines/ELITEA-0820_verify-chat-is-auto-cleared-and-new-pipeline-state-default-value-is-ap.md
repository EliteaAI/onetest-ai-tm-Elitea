---
id: ELITEA-0820
title: "Verify chat is auto-cleared and new pipeline state default value is applied immediately after saving changes"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3502]
---
# ELITEA-0820: Verify chat is auto-cleared and new pipeline state default value is applied immediately after saving changes

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that after modifying and saving a pipeline state's default value, the chat conversation is automatically cleared and the new default value is immediately applied in the subsequent run — without requiring a manual page reload.

**Coverage:**
- Changing a pipeline state default value triggers automatic chat clearing
- After auto-clear, the new default value is used in the next pipeline run
- No manual page reload is needed for the change to take effect
- Behavior consistency for any pipeline configuration change (not just default value)

## Preconditions

- User is logged in at {{base_url}}
- A pipeline with at least one custom state exists (or will be created during the test)
- The pipeline's chat/run area is visible and active

## Test Data

- Pipeline name: any existing or new pipeline
- State name: myState
- State data type: String
- Initial default value: old_value
- Updated default value: new_value
- Printer node type: Variable, selected state: myState

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines from the sidebar. Open an existing pipeline or create a new one. | Pipeline configuration view is displayed. |
| 2 | Create a custom state named 'myState' (type: String) with default value set to 'old_value'. Add a Printer node, set its type to Variable, and select 'myState' as the variable source. Save the pipeline. | State 'myState' is saved with default value 'old_value'. Printer node is configured to output the state value. |
| 3 | Execute the pipeline. Observe the Printer node output in the chat. | Pipeline runs. The Printer node outputs 'old_value'. |
| 4 | Change the default value of 'myState' from 'old_value' to 'new_value'. Click Save. | Changes are saved. The chat/run area is automatically cleared — a new conversation is started without any manual action. |
| 5 | Confirm that the chat area shows a fresh/empty conversation state (no history from the previous run). Do NOT reload the page. | The chat history is cleared and a new session is visible. No manual page reload was performed. |
| 6 | Execute the pipeline again. Observe the Printer node output in the chat. | Pipeline runs. The Printer node outputs 'new_value'. |
| 7 | Edge case: Make another configuration change (e.g., change the state default value again to 'another_value'). Click Save. | The chat is cleared again automatically after saving. Each pipeline configuration save triggers an auto-clear. |

## Expected Final State

The chat is cleared again automatically after saving. Each pipeline configuration save triggers an auto-clear.

## Pass/Fail Criteria

**Pass:**
- After saving the default value change, the chat is automatically cleared without any user action
- The pipeline run in the new session outputs 'new_value' (not 'old_value')
- No page reload is needed at any point
- Any further configuration change also triggers auto-clear

**Fail:**
- The chat is NOT cleared after saving — old conversation persists
- The pipeline still outputs 'old_value' after save (old behavior)
- Auto-clear only happens for some change types but not default value changes
- A manual page reload is still required for the new value to take effect
