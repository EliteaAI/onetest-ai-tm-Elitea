---
id: ELITEA-0819
title: "Verify pipeline state default value changed via Chat Canvas is applied immediately in the next run"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, feat:chat]
requirements: [ProjectAlita/projectalita.github.io#3866]
---
# ELITEA-0819: Verify pipeline state default value changed via Chat Canvas is applied immediately in the next run

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a pipeline state's default value is changed via the Chat Canvas Flow view and saved, the new value is used immediately in the next pipeline run — without requiring a chat clear or page reload.

**Coverage:**
- Editing pipeline state default value via Chat Canvas and saving applies the new value immediately
- The next pipeline run in the same chat session uses the new default value
- No chat clear, page reload, or reattach is needed for the change to take effect
- Changing the value a second time also takes effect immediately in the subsequent run

## Preconditions

- User is logged in at {{base_url}}
- A pipeline with a custom state and a Printer node (type: Variable, source: the state) exists
- The pipeline is attached to a chat
- Initial default value of the state is set to `old_value`

## Test Data

- Pipeline name: any existing pipeline with a custom state and a Printer node
- State name: `myState`
- State data type: String
- Initial default value: `old_value`
- Updated default value: `new_value`
- Second updated value: `another_value`
- Printer node type: Variable, selected state: `myState`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from the sidebar. Open or create a chat that has the pipeline attached. | Chat view is displayed with the pipeline available. |
| 2 | Execute the pipeline. Observe the Printer node output. | Pipeline runs. The Printer node outputs `old_value`. |
| 3 | Open the Canvas for the pipeline from the chat. Switch to the Flow view. | The pipeline Flow view is visible inside the Chat Canvas. |
| 4 | Change the default value of `myState` from `old_value` to `new_value`. Click Save. | Changes are saved. The chat is not cleared — the same conversation remains active. |
| 5 | Without clearing the chat or reloading the page, execute the pipeline again. Observe the Printer node output. | The Printer node outputs `new_value`. The new default value is applied immediately in the same chat session. |
| 6 | Open the Canvas again. Change the default value of `myState` from `new_value` to `another_value`. Click Save. | Changes are saved. The chat session remains active. |
| 7 | Without clearing the chat or reloading the page, execute the pipeline again. Observe the Printer node output. | The Printer node outputs `another_value`. The second value change also takes effect immediately. |

## Expected Final State

The Printer node outputs `another_value`. The second value change also takes effect immediately.

## Pass/Fail Criteria

**Pass:**
- After saving the new default value via Chat Canvas, the very next pipeline run outputs `new_value` — without clearing the chat or reloading the page
- A second value change via Chat Canvas also takes effect immediately in the next run
- No manual intervention (chat clear, page reload, reattach) is required at any point

**Fail:**
- The pipeline still outputs `old_value` after saving the new default value via Chat Canvas (change not applied immediately)
- The new value only takes effect after clearing the chat or reloading the page (regression of bug #3866)
