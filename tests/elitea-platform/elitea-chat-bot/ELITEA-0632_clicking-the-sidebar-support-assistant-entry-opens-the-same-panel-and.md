---
id: ELITEA-0632
title: "Clicking the sidebar Support Assistant entry opens the same panel and conversation as the floating launcher"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [session-sharing, entry-point, same-widget, smoke]
requirements: [#4780]
---
# ELITEA-0632: Clicking the sidebar Support Assistant entry opens the same panel and conversation as the floating launcher

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Both the sidebar entry and the floating launcher must open the same Support Assistant panel showing the same conversation. If each entry point opens a separate instance or a different session, the user will have a fragmented and confusing experience.

## Preconditions

Logged in to ELITEA ({{base_url}}
Support Assistant feature is enabled
At least one message has been sent in the current session

## Test Data

Active conversation with at least one message and response

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Support Assistant using the floating launcher icon and send a message. Wait for the response. Note the message text. | Conversation contains the sent message and the assistant response. |
| 2 | Click the X button to close the panel. | Panel closes. The launcher icon is visible at the sidebar bottom. |
| 3 | Click the "Support Assistant" entry at the bottom of the sidebar. | The panel opens. |
| 4 | Observe the conversation in the panel. | The same message and response from step 1 are present — identical session, same content, same order. |
| 5 | Close the panel using the X button. | Panel closes. |
| 6 | Reopen the panel using the floating launcher icon. | Same conversation is shown again. |

## Expected Final State

Same conversation is shown again.

## Pass/Fail Criteria

Pass: Both entry points show the same conversation in the same panel; No duplicate panels open simultaneously; No separate or empty session opens from either entry point.
Fail: Sidebar entry and launcher open different instances with different conversations; Two separate panels open when using both entry points; Sidebar entry opens a blank new session while launcher shows the existing conversation.
