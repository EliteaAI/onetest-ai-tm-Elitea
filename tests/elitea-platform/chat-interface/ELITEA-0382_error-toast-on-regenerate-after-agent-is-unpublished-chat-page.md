---
id: ELITEA-0382
title: "Error Toast on Regenerate After Agent is Unpublished (Chat Page)"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4721]
---
# ELITEA-0382: Error Toast on Regenerate After Agent is Unpublished (Chat Page)

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking Regenerate on a message produced by a now-unpublished agent displays an error toast and preserves the previous response.

**Coverage:**
- Initial response is received from a published agent in Chat
- Agent is unpublished after the response is received
- Regenerate triggers a server error
- Error toast appears with the correct message
- Previous response remains visible (no blank state)
- Toast is visible for ≥5 seconds or until dismissed

## Preconditions

- Logged in to {{base_url}}
- A published agent exists in the project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Chat page. Add the published agent as a participant. Send a message and wait for the agent's response. | Agent returns a response. The response is visible in the chat. |
| 2 | Navigate to the Agents page and unpublish the agent. | Agent status changes to unpublished. |
| 3 | Return to the chat conversation from step 1. | Chat is still open. The previous agent response is visible. |
| 4 | Click the Regenerate button on the agent's message. | Regeneration request is sent to the server. Server returns an error (unpublished agent). |
| 5 | Observe the UI after the request completes. | Error toast appears with the message "Regeneration Failed. Please try again." |
| 6 | Observe the toast visibility duration. | Toast remains visible for at least 5 seconds or until manually dismissed. |
| 7 | Observe the chat message area. | The previous agent response is still displayed. No blank or empty state appears. |

## Expected Final State

The previous agent response is still displayed. No blank or empty state appears.

## Pass/Fail Criteria

**Pass:**
- Error toast appears with "Regeneration Failed. Please try again."
- Toast is visible for ≥5 seconds or until dismissed
- Previous response is preserved in the chat

**Fail:**
- No toast appears — silent failure
- Toast appears with incorrect or missing text
- Previous response disappears or is replaced with a blank state
