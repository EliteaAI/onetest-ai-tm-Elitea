---
id: ELITEA-0637
title: "Conversation auto-scrolls to the latest message after each new exchange"
priority: medium
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [scroll-behavior, auto-scroll, R-2.0.3, ux]
requirements: [EliteaAI/elitea_issues#4775]
---
# ELITEA-0637: Conversation auto-scrolls to the latest message after each new exchange

**Module:** Elitea Chat Bot · **Priority:** Medium · **Type:** Functional

**Objective:** After each new message or response, the conversation must automatically scroll to show the latest content. If the user scrolls up to read earlier messages, the view must not jump back down until the user sends a new message.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- Support Assistant panel is open with at least 6–8 message exchanges already present so the conversation list is tall enough to require scrolling

## Test Data

- Use an existing conversation with many messages, or send 5+ messages to build up scroll height

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send a new message and wait for the assistant response. | After the response appears, the conversation view is scrolled to the bottom showing the latest message. |
| 2 | Manually scroll up using the mouse wheel to view earlier messages from the top of the conversation. | Older messages become visible. The view stays scrolled to where the user stopped. It does not auto-jump back down mid-read. |
| 3 | While scrolled up, send a new message. | The conversation immediately scrolls back down to show the newly sent user message. |
| 4 | Wait for the assistant response to appear. | The view stays at the bottom as the response streams in, so the user sees it as it arrives. |

## Expected Final State

The view stays at the bottom as the response streams in, so the user sees it as it arrives.

## Pass/Fail Criteria

Pass:
- View scrolls to bottom after each new message/response
- View holds position while user is reading older messages (no unwanted auto-scroll)
- Sending a new message scrolls the view back to the bottom

Fail:
- New messages appear off-screen and user must manually scroll to see them
- View jumps to the bottom while the user is reading older messages
- View does not scroll to bottom after a new message is sent
