---
id: ELITEA-2368
title: "Catalog — E2E start conversation with agent that has no conversation starters, type and send message, receive reply"
priority: medium
type: functional
module: agent-hub
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
---

# ELITEA-2368: Catalog — E2E start conversation with agent that has no conversation starters, type and send message, receive reply

**Module:** agent-hub · **Priority:** medium · **Type:** functional

**Objective:** Verify that Catalog — E2E start conversation with agent that has no conversation starters, type and send message, receive reply. Success is confirmed when verify the context budget counter in the bottom right updates (if context managment is active).

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
| 1 | Navigate to Catalog (the Agents tab is active) | Catalog loads on the Agents tab (selected). |
| 2 | Click on an agent card that shows "No predefined conversation starters" (e.g., "Business Analyst") | Control responds; expected next state is shown. |
| 3 | Verify the detail modal opens displaying agent name, description, "CONVERSATION STARTERS" section with text "No predefined conversation starters – just type your request to begin" and "WELCOME MESSAGE" section with text "No welcome message set – the agent will start without a greeting" | Condition holds as described. |
| 4 | Click the "Start conversation" button | Control responds; expected next state is shown. |
| 5 | Verify a new chat is created and the user is redirected to the Chat interface | Condition holds as described. |
| 6 | Verify the welcome message "Hello, [user]! What can I do for you today?" is displayed in the chat area | Condition holds as described. |
| 7 | Verify the agent chip (e.g., "Business Analyst v2.1") is visible in the message input bar | Condition holds as described. |
| 8 | Verify the agent appears under the AGENTS section in the Participants panel on the right | Condition holds as described. |
| 9 | Click the message input field and type a message (e.g., "execute agent") | Control responds; expected next state is shown. |
| 10 | Verify the typed text appears in the input field and the send button becomes active | Condition holds as described. |
| 11 | Click the send button | Control responds; expected next state is shown. |
| 12 | Verify the user message is displayed in the chat as sent | Condition holds as described. |
| 13 | Verify the agent begins processing (e.g., "Thought for X secs" indicator is shown) | Condition holds as described. |
| 14 | Verify the agent reply is received and displayed in the chat | Condition holds as described. |
| 15 | Verify the new conversation appears in the chat list in the left sidebar under "Today" | Condition holds as described. |
| 16 | Verify the Context Budget counter in the bottom right updates (if context managment is active) | Condition holds as described. |

---

## Expected Final State

Verify the Context Budget counter in the bottom right updates (if context managment is active).

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Catalog — E2E start conversation with agent that has no conversation starters, type and send message, receive reply.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
