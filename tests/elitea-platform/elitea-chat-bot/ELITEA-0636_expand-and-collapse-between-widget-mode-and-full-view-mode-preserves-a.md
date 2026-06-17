---
id: ELITEA-0636
title: "Expand and collapse between widget mode and full-view mode preserves all conversation content"
priority: medium
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [content-preservation, expand-collapse, display-modes, R-2.0.3]
requirements: [#4775, #4774]
---
# ELITEA-0636: Expand and collapse between widget mode and full-view mode preserves all conversation content

**Module:** Elitea Chat Bot · **Priority:** Medium · **Type:** Functional

**Objective:** Switching between compact widget mode and the expanded full-view overlay must not lose any messages or reset the session. A user who expands the panel to read a long response should see the same conversation when they collapse back.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- Support Assistant panel is open in compact widget mode with at least one message exchange visible

## Test Data

- Existing conversation with at least 2 messages in compact widget mode

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Note the messages currently visible in the compact widget. | Messages noted for comparison. |
| 2 | Click the Expand button in the panel header. | The panel expands into a large full-view overlay covering most of the screen. |
| 3 | Verify that all the messages noted in step 1 are visible in the expanded view. | All prior messages are present. No content is missing. |
| 4 | Send a new message while in expanded mode and wait for the response. | The message and response appear normally in the expanded view. |
| 5 | Click the Expand/collapse button again to return to compact widget mode. | The panel shrinks back to the compact widget size. |
| 6 | Verify that all messages — including the one sent in step 4 — are visible in compact mode. | All messages are present. No content was lost during the expand/collapse cycle. |

## Expected Final State

All messages are present. No content was lost during the expand/collapse cycle.

## Pass/Fail Criteria

Pass:
- Same messages visible in both compact and expanded modes
- Message sent in expanded mode is retained after collapsing
- No flash, blank state, or loading on mode switch

Fail:
- Messages disappear or reset when switching between modes
- Message sent in expanded mode is missing after collapse
- A blank or loading state appears on expand or collapse
