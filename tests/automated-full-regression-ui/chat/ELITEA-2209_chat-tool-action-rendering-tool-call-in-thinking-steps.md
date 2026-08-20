---
id: ELITEA-2209
title: "Chat – Tool Action Rendering – Verify Tool Call Displays in Thinking Steps When Toolkit Called Directly"
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

# ELITEA-2209: Chat – Tool Action Rendering – Verify Tool Call Displays in Thinking Steps When Toolkit Called Directly

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that when a toolkit is called directly (without an agent), the tool call appears in the LLM's thinking steps.

---

## Preconditions

- User is logged in to the Elitea platform.
- A toolkit (e.g. 'aaa') is added as participant.

---

## Test Data

| Field | Value |
|-------|-------|
| Message | create_file |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Add toolkit 'aaa' via + > Toolkits (no agent added) | Toolkit in PARTICIPANTS; no AGENTS section |
| 2 | Send a message that triggers a tool call (e.g. 'create_file') | LLM processes; 'Thought for X secs' indicator appears |
| 3 | Expand 'Thought for X secs' section | Thinking steps show the tool call |
| 4 | Verify tool call shown as chip with format 'toolkit_name.tool_name' (e.g. 'aaa: create_file') | Tool call chip visible with icon |

---

## Expected Final State

Tool call visible in thinking steps when toolkit called directly.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Tool call shown in thinking steps.

**Fail:**
- Any step produces an error or unexpected result.
- Tool call not visible in thinking steps.
