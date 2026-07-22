---
id: ELITEA-2468
title: "Chat – Select MCP from / dropdown"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2468: Chat – Select MCP from / dropdown

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that Chat – Select MCP from / dropdown. Success is confirmed when verify if the mcp has available tools they are displayed in a tools list; if no tools or disconnected, no tools list appears.

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
| 1 | Navigate to the Chats section with a conversation that has an MCP added as participant (e.g. "delete") | Target page/section loads successfully. |
| 2 | Type "/" in the message input field and verify the dropdown shows the MCP | Field accepts the input and displays the entered value. |
| 3 | Click on "delete" in the dropdown and verify the message input shows "/delete" | Control responds; expected next state is shown. |
| 4 | Verify if the MCP has available tools they are displayed in a tools list; if no tools or disconnected, no tools list appears | Condition holds as described. |

---

## Expected Final State

Verify if the MCP has available tools they are displayed in a tools list; if no tools or disconnected, no tools list appears.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – Select MCP from / dropdown.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
