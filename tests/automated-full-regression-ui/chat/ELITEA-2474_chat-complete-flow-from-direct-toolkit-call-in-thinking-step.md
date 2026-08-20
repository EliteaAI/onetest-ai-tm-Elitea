---
id: ELITEA-2474
title: "Chat – Complete flow from direct toolkit call in thinking steps to output chip display"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: "tests.ui.chat.test_direct_toolkit_call_complete_flow.TestDirectToolkitCallCompleteFlow.test_direct_toolkit_call_complete_flow"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1608
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2474: Chat – Complete flow from direct toolkit call in thinking steps to output chip display

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that Chat – Complete flow from direct toolkit call in thinking steps to output chip display. Success is confirmed when verify the llm's response text follows below the chips describing the tool execution result.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Chats section and create a new conversation with only a toolkit participant (no agent) | Target page/section loads successfully. |
| 2 | Send a message requesting a tool action (e.g. "create a file named test.txt") | Action completes without error and produces the expected UI state. |
| 3 | Verify "Thought for X secs" indicator appears; expand and verify the tool call is shown with format "toolkit_name.tool_name" | Condition holds as described. |
| 4 | After tool execution, verify the LLM's response appears in the conversation | Action completes without error and produces the expected UI state. |
| 5 | Verify tool execution chips are displayed at the top of the response: LLM model chip, toolkit chip, and tool call chip | Condition holds as described. |
| 6 | Verify chips are horizontal in a row with appropriate icons and labels | Condition holds as described. |
| 7 | Verify the LLM's response text follows below the chips describing the tool execution result | Condition holds as described. |

---

## Expected Final State

Verify the LLM's response text follows below the chips describing the tool execution result.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – Complete flow from direct toolkit call in thinking steps to output chip display.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
