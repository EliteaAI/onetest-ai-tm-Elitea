---
id: ELITEA-0638
title: "Long assistant responses display fully without breaking the panel layout"
priority: medium
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [long-response, overflow, R-2.0.3, layout]
requirements: [EliteaAI/elitea_issues#4775]
---
# ELITEA-0638: Long assistant responses display fully without breaking the panel layout

**Module:** Elitea Chat Bot · **Priority:** Medium · **Type:** Functional

**Objective:** Users asking detailed questions receive long, multi-paragraph responses. These must wrap cleanly inside the message bubble and not overflow the panel boundaries, cause horizontal scrollbars, or cut off any content.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- Support Assistant panel is open in compact (widget) mode

## Test Data

- Message: "Give me a full step-by-step guide to setting up ELITEA from scratch, including all configuration options and best practices"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type the test message and send it. | Message submitted. Loading indicator shows. |
| 2 | Wait for the full response to render. | A long multi-paragraph response appears in the assistant message bubble. |
| 3 | Observe the response text relative to the panel boundaries. | All text wraps within the message bubble. No text overflows horizontally outside the panel. |
| 4 | Check whether a horizontal scrollbar appears on the panel or message list. | No horizontal scrollbar is present. |
| 5 | Scroll vertically through the full response. | The complete response is accessible by scrolling. No content is cut off at the bottom. |
| 6 | Click the Expand button to open the full-view mode and check the same response. | The full response is equally readable in expanded mode. No layout breaks. |

## Expected Final State

The full response is equally readable in expanded mode. No layout breaks.

## Pass/Fail Criteria

Pass:
- All response text wraps within the panel
- No horizontal overflow or horizontal scrollbar
- Full response accessible by vertical scrolling in both compact and expanded modes

Fail:
- Text overflows outside the panel boundaries
- A horizontal scrollbar appears
- Content is cut off and cannot be accessed by scrolling
