---
id: ELITEA-0649
title: "Support Assistant shows the configured welcome message when opened for the first time"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [welcome-message, initial-state, regression, R-2.0.3, smoke]
requirements: [EliteaAI/elitea_issues#4775, EliteaAI/elitea_issues#4773]
---
# ELITEA-0649: Support Assistant shows the configured welcome message when opened for the first time

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** A user opening the Support Assistant for the very first time should see only the configured welcome message — no history, no prior messages from anyone else. Verifies correct first-time session initialization and that the welcome message content matches what the admin has configured.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- Support Assistant is enabled in Admin → Guardrails → Support Assistant (toggle is ON)
- A welcome message is configured by admin (e.g., "Hi! I'm your ELITEA Support Assistant. Ask me anything about ELITEA or report any issues you're experiencing.")
- The test user has no prior support conversation history — use a freshly created user account or a user who has never interacted with the Support Assistant

## Test Data

- Test user: fresh account with zero support conversation history
- Expected welcome message text: as configured in Admin → Guardrails → Support Assistant

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the ELITEA Chat page. | The Chat page loads without errors. The sidebar is visible on the left. |
| 2 | Locate the Support Assistant launcher icon at the very bottom of the sidebar (purple circle icon). Click it. | The Support Assistant panel opens as a floating widget on the screen. |
| 3 | Observe the message area inside the opened panel. | The configured welcome message is displayed as an assistant message. No user messages are present. No history from any other session appears. |
| 4 | Verify that the welcome message text matches the text configured by the admin in Guardrails. | The message content is exactly as configured — no default placeholder text, no empty message area. |
| 5 | Observe the message input field at the bottom of the panel. | The input field is visible with placeholder text "Type a message..." and is ready to accept typing. |

## Expected Final State

The input field is visible with placeholder text "Type a message..." and is ready to accept typing.

## Pass/Fail Criteria

Pass:
- Welcome message is displayed immediately on open and matches the admin-configured text exactly
- No prior user messages or conversation history from any session is visible
- Input field is present and accepts typing

Fail:
- Welcome message is missing or shows incorrect/default text
- Messages from another user's session or a previous session bleed into the view
- Panel fails to open or shows an error state
