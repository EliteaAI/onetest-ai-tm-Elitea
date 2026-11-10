---
id: ELITEA-2369
title: "Catalog — E2E start conversation with agent that has conversation starters, use starter to send message, receive reply"
priority: medium
type: functional
module: agent-hub
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
---

# ELITEA-2369: Catalog — E2E start conversation with agent that has conversation starters, use starter to send message, receive reply

**Module:** agent-hub · **Priority:** medium · **Type:** functional

**Objective:** Verify that Catalog — E2E start conversation with agent that has conversation starters, use starter to send message, receive reply. Success is confirmed when verify the agent begins processing (e.g., "thought for x secs" indicator is shown) and tools used are visible.

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
| 2 | Click on an agent card that has predefined conversation starters (e.g., "API Testing Buddy") | Control responds; expected next state is shown. |
| 3 | Verify the detail modal opens displaying agent name and description | Condition holds as described. |
| 4 | Verify the "CONVERSATION STARTERS" section displays multiple predefined starter options | Condition holds as described. |
| 5 | Verify the "WELCOME MESSAGE" section displays the agent's configured welcome text (e.g., "Welcome! I'm your API Testing Buddy—ready to validate documentation...") | Condition holds as described. |
| 6 | Click the "Start conversation" button | Control responds; expected next state is shown. |
| 7 | Verify a new chat is created and the user is redirected to the Chat interface | Condition holds as described. |
| 8 | Verify the conversation starters are displayed as clickable suggestion tiles in the chat area | Condition holds as described. |
| 9 | Verify the agent chip (e.g., "API Testing Buddy v1.1") is visible in the message input bar | Condition holds as described. |
| 10 | Verify the agent appears under the AGENTS section in the Participants panel on the right | Condition holds as described. |
| 11 | Click one of the conversation starter tiles (e.g., "I've uploaded a Swagger spec—can you confirm tooling readiness and outline the test plan?") | Control responds; expected next state is shown. |
| 12 | Verify the selected starter text is populated into the message input field | Condition holds as described. |
| 13 | Verify the send button becomes active | Condition holds as described. |
| 14 | Click the send button | Control responds; expected next state is shown. |
| 15 | Verify the message is sent and displayed in the chat | Condition holds as described. |
| 16 | Verify the agent begins processing (e.g., "Thought for X secs" indicator is shown) and tools used are visible | Condition holds as described. |

---

## Expected Final State

Verify the agent begins processing (e.g., "Thought for X secs" indicator is shown) and tools used are visible.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Catalog — E2E start conversation with agent that has conversation starters, use starter to send message, receive reply.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
