---
id: ELITEA-2472
title: "Chat – HITL Block button prevents toolkit tool from executing"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2472: Chat – HITL Block button prevents toolkit tool from executing

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that Chat – HITL Block button prevents toolkit tool from executing. Success is confirmed when verify the llm responds indicating the action was blocked or not performed.

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
| 3 | Click the Block button (red with X) | Control responds; expected next state is shown. |
| 4 | Verify the authorization card closes or updates to show the action was blocked | Condition holds as described. |
| 5 | Verify the LLM does NOT execute the sensitive toolkit tool | Condition holds as described. |
| 6 | Verify no tool execution chips appear for the blocked tool | Condition holds as described. |
| 7 | Verify the LLM responds indicating the action was blocked or not performed | Condition holds as described. |

---

## Expected Final State

Verify the LLM responds indicating the action was blocked or not performed.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – HITL Block button prevents toolkit tool from executing.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
