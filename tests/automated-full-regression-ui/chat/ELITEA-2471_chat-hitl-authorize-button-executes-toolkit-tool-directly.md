---
id: ELITEA-2471
title: "Chat – HITL Authorize button executes toolkit tool directly"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2471: Chat – HITL Authorize button executes toolkit tool directly

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that Chat – HITL Authorize button executes toolkit tool directly. Success is confirmed when verify tool execution chips appear (llm model, toolkit, tool call) and the conversation continues normally.

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
| 1 | Navigate to a conversation with only a HITL toolkit participant and trigger a sensitive action | Target page/section loads successfully. |
| 2 | Verify the "Sensitive Action Authorization Required" card appears | Condition holds as described. |
| 3 | Click the Authorize button (green with checkmark) | Control responds; expected next state is shown. |
| 4 | Verify the authorization card closes or updates to show authorization was granted | Condition holds as described. |
| 5 | Verify the LLM proceeds to execute the authorized toolkit tool directly | Condition holds as described. |
| 6 | Verify tool execution chips appear (LLM model, toolkit, tool call) and the conversation continues normally | Condition holds as described. |

---

## Expected Final State

Verify tool execution chips appear (LLM model, toolkit, tool call) and the conversation continues normally.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – HITL Authorize button executes toolkit tool directly.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
