---
id: ELITEA-2853
title: "ask_user - Cancelling clarifying question flow gracefully aborts agent execution"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [chat, hitl, internal-tools, ask-user, issue:6095]
requirements: [EliteaAI/elitea_issues#6095]
---

# ELITEA-2853: ask_user - Cancelling clarifying question flow gracefully aborts agent execution

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify cancelling the clarifying question flow gracefully aborts agent execution without errors.

## Preconditions

- User is logged in to `{{base_url}}`
- ask_user tool is enabled
- Agent has triggered ask_user with questions

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger ask_user with multiple questions | Clarifying question card appears |
| 2 | Answer first question | Answer recorded |
| 3 | Navigate to second question | Question 2 appears |
| 4 | Locate Cancel button on the card | Cancel button is visible |
| 5 | Click Cancel button | Confirmation dialog appears (if applicable) |
| 6 | Confirm cancellation | Card closes immediately |
| 7 | Verify agent execution is aborted | No agent response is generated |
| 8 | Verify chat interface returns to normal state | Input field is enabled, no pending operations |
| 9 | Send a new message | New message is processed normally |
| 10 | Verify previous partial answers are not persisted | Previous session is clean |

## Expected Final State

Cancellation aborts agent execution gracefully, card closes, chat returns to ready state, no errors or hanging state.

## Pass/Fail Criteria

**Pass:** Cancel button works, agent execution aborted, chat returns to normal, no errors

**Fail:** Cancel button missing or non-functional, agent continues execution, errors occur, chat hangs
