---
id: ELITEA-1938
title: "Remote MCP — Test Settings — Clear Chat"
priority: medium
type: functional
module: elitea-platform
status: draft
execution_type: manual
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1938: Remote MCP — Test Settings — Clear Chat

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the "clear the chat" button in the Test Settings panel removes all messages from the chat area.

---

## Preconditions

- User is logged in to the Elitea platform.
- A Remote MCP with Test Settings panel is available.
- At least one tool run has been performed to produce a chat message.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a Remote MCP with Test Settings panel | Detail page loads with Test Settings panel |
| 2 | Run a tool to generate at least one response message in chat | At least one message is visible in the chat area |
| 3 | Verify at least one response message is visible in chat area | Message is confirmed visible |
| 4 | Click "clear the chat" button (trash icon) | Clear action is triggered |
| 5 | Verify all messages are removed from chat area | Chat area is empty |
| 6 | Verify welcome message reappears (or chat is blank) | Welcome message is shown or chat is blank |

---

## Expected Final State

All chat messages are removed and the chat area is empty or shows the welcome message after clearing.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All messages are cleared from the chat area.

**Fail:**
- Any step produces an error or unexpected result.
- Messages remain after clicking the clear button.
