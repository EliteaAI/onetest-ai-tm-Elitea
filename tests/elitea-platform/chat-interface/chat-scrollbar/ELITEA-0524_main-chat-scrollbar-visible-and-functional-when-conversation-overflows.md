---
id: ELITEA-0524
title: "Main Chat — scrollbar visible and functional when conversation overflows the viewport"
priority: medium
type: functional
module: chat-scrollbar
status: ready
execution_type: manual
tags: [feat:toolkits, issue:3704, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3704]
---
# ELITEA-0524: Main Chat — scrollbar visible and functional when conversation overflows the viewport

**Module:** Chat Scrollbar · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a scrollbar is visible and functional in the Main Chat conversation area when AI responses overflow the visible container height.

**Coverage:**
- Scrollbar appears on the right edge of the chat conversation area when content overflows
- Dragging the scrollbar thumb scrolls the conversation
- Mouse wheel scrolling works within the conversation area
- All message content is reachable by scrolling to the bottom

## Preconditions

- Logged in to {{base_url}}
- Main Chat accessible from the sidebar
- A model is selected (e.g., Anthropic Claude Haiku 4.5)
- Chrome or Edge, latest stable

## Test Data

- Prompt: `"List 50 programming languages with their main use cases, year of creation, and key features"`
- Model: any configured LLM (e.g., Anthropic Claude Haiku 4.5)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from the sidebar. Start a new conversation. | Chat interface opens with an empty conversation area. |
| 2 | Send a prompt that generates a long multi-paragraph response, e.g.: "List 50 programming languages with their main use cases, year of creation, and key features." | AI generates a long response that exceeds the visible chat container height. |
| 3 | Observe the right edge of the conversation area. | A scrollbar is visible on the right side of the chat container. |
| 4 | Click and drag the scrollbar thumb upward, then downward. | Conversation content scrolls up and down in sync with the thumb position. |
| 5 | Place the mouse cursor over the conversation area and use the mouse wheel to scroll. | Content scrolls smoothly using the mouse wheel. |
| 6 | Scroll to the very bottom of the conversation. | The most recent AI response is fully visible; no content is cut off below the visible area. |

## Expected Final State

The most recent AI response is fully visible; no content is cut off below the visible area.

## Pass/Fail Criteria

**Pass:**
- Scrollbar is visible when conversation content overflows the viewport
- Dragging thumb and mouse wheel both scroll content correctly
- All content reachable at the bottom of the scroll

**Fail:**
- No scrollbar visible despite conversation content overflowing
- Scrollbar present but dragging or wheel scroll has no effect
- Bottom of conversation unreachable
