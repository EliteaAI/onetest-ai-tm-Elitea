---
id: ELITEA-0629
title: "An open Support Assistant conversation is retained when the user navigates between pages"
priority: medium
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [state-persistence, cross-page, navigation]
requirements: [EliteaAI/elitea_issues#4780, EliteaAI/elitea_issues#4774]
---
# ELITEA-0629: An open Support Assistant conversation is retained when the user navigates between pages

**Module:** Elitea Chat Bot · **Priority:** Medium · **Type:** Functional

**Objective:** If a user is mid-conversation in the Support Assistant and navigates to another section of the application, the conversation must still be there when they look back at the panel. Losing the conversation on a page navigation is a disorienting and potentially frustrating defect.

## Preconditions

Logged in to ELITEA ({{base_url}}
Support Assistant panel is open with an active conversation (at least one message and response visible)

## Test Data

Message: "This message should survive page navigation"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Support Assistant panel from the sidebar entry. | Panel is open. |
| 2 | Type "This message should survive page navigation" and send it. Wait for the assistant response. | The full exchange is visible in the conversation. |
| 3 | Keep the panel open and click Agents in the sidebar navigation. | The Agents page loads in the main content area. The Support Assistant panel remains open and visible, still showing the same conversation. |
| 4 | Click Pipelines in the sidebar navigation. | Pipelines page loads. The Support Assistant panel is still open with the same conversation intact. |
| 5 | Click the X button to close the panel and then navigate to the Chat page. | Panel closes. Chat page loads. |
| 6 | Click the Support Assistant sidebar entry to reopen the panel. | The panel opens and shows the same conversation with the test message and its response still present. |

## Expected Final State

The panel opens and shows the same conversation with the test message and its response still present.

## Pass/Fail Criteria

Pass: Conversation is visible and intact after navigating between pages while the panel is open; Closing and reopening the panel after navigation still shows the same session.
Fail: Conversation resets or clears when navigating to another page; The panel shows an empty or new session after page navigation; Messages are lost when the panel is closed and reopened after navigation.
