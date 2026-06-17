---
id: ELITEA-0521
title: "Pipeline Chat panel — scrollbar visible and functional when messages overflow the panel"
priority: medium
type: functional
module: chat-scrollbar
status: ready
execution_type: manual
tags: [feat:toolkits, issue:3704, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3704]
---
# ELITEA-0521: Pipeline Chat panel — scrollbar visible and functional when messages overflow the panel

**Module:** Chat Scrollbar · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a scrollbar is visible and functional in the Pipeline chat output panel when messages overflow the visible panel height.

**Coverage:**
- Scrollbar appears on the right edge of the Pipeline chat panel when message content overflows
- Dragging the scrollbar thumb scrolls the chat content
- Mouse wheel scrolling works within the Pipeline chat panel
- All exchange history is reachable by scrolling

## Preconditions

- Logged in to {{base_url}}
- A Pipeline exists with at least one execution that has produced a multi-turn chat output (e.g., a pipeline containing an Agent or LLM node with chat history enabled)
- Pipeline chat panel is accessible within the Pipeline editor
- Chrome or Edge, latest stable

## Test Data

- Pipeline: any pipeline with a visible chat panel (Agent toolkit node or LLM node with chat history)
- Target: 5+ message exchanges to overflow the panel height

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines. Open a Pipeline that includes a chat output panel (e.g., a Pipeline with an Agent Toolkit node). The panel should show the chat area on the right side of the editor. | Pipeline editor opens with the chat panel visible on the right. |
| 2 | Send several messages to the pipeline chat to build up a conversation history longer than the panel height. For example, send 5+ messages with verbose responses. | Multiple user and AI messages fill the chat panel and the total height exceeds the visible panel area. |
| 3 | Observe the right edge of the Pipeline chat panel. | A scrollbar is visible on the right edge of the panel. |
| 4 | Click and drag the scrollbar thumb to scroll up and down through the conversation. | Content scrolls up and down correctly with the thumb. |
| 5 | Use the mouse wheel while hovering over the chat panel. | Content scrolls smoothly with the mouse wheel. |
| 6 | Scroll to the bottom of the panel. | The most recent message is fully visible with no content cut off. |

## Expected Final State

The most recent message is fully visible with no content cut off.

## Pass/Fail Criteria

**Pass:**
- Scrollbar appears in the Pipeline chat panel when content overflows
- Thumb drag and mouse wheel both scroll correctly
- Full conversation history browsable by scrolling

**Fail:**
- No scrollbar despite overflowing content in the Pipeline chat panel
- Content inaccessible — no scroll mechanism available
- Scrollbar non-functional (visible but does not scroll)
