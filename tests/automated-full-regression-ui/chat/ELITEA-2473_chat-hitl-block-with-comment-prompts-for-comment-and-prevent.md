---
id: ELITEA-2473
title: "Chat – HITL Block with Comment prompts for comment and prevents tool execution"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2473: Chat – HITL Block with Comment prompts for comment and prevents tool execution

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that Chat – HITL Block with Comment prompts for comment and prevents tool execution. Success is confirmed when verify the llm does not execute the sensitive toolkit tool and may reference the provided comment.

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
| 3 | Click the Block with Comment button (gray) | Control responds; expected next state is shown. |
| 4 | Verify a modal or text input appears prompting for a comment | Condition holds as described. |
| 5 | Type a comment (e.g. "This action is too risky and could delete important data") | Field accepts the input and displays the entered value. |
| 6 | Click Submit or Confirm | Control responds; expected next state is shown. |
| 7 | Verify the modal closes and the action was blocked with comment | Condition holds as described. |
| 8 | Verify the LLM does NOT execute the sensitive toolkit tool and may reference the provided comment | Condition holds as described. |

---

## Expected Final State

Verify the LLM does NOT execute the sensitive toolkit tool and may reference the provided comment.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – HITL Block with Comment prompts for comment and prevents tool execution.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
