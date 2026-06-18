---
id: ELITEA-0590
title: "History panel layout is correct in expanded widget view"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4778]
requirements: [EliteaAI/elitea_issues#4778]
---
# ELITEA-0590: History panel layout is correct in expanded widget view

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify the history panel renders without layout issues when the widget is in expanded (full) mode.

**Coverage:**
- No overflow, hidden controls, or clipped content
- Panel scrollable in expanded view

## Preconditions

- Logged in on {{base_url}}
- Widget is expanded (.elitea-assistant-window--expanded)
- 3+ sessions in history

## Test Data

- Expanded widget dimensions: 720x646 px (based on observed viewport)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Support Assistant and click 'Expand chat' button | Widget enlarges to expanded mode |
| 2 | Click 'Chat history' (🕐) icon | History panel opens within the expanded layout |
| 3 | Inspect the panel: scroll, all items visible, no clipping | All sessions are visible, panel is fully scrollable, no elements overflow outside boundaries |
| 4 | Click a session | Session loads correctly in the expanded view |

## Expected Final State

Session loads correctly in the expanded view

## Pass/Fail Criteria

**Pass:**
- History panel fully usable in expanded mode
- No visual layout defects

**Fail:**
- Panel overflows widget boundaries in expanded mode
- Sessions cut off or controls hidden
