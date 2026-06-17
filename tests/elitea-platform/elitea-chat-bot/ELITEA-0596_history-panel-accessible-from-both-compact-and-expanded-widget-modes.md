---
id: ELITEA-0596
title: "History panel accessible from both compact and expanded widget modes"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4778]
requirements: [EliteaAI/elitea_issues#4778]
---
# ELITEA-0596: History panel accessible from both compact and expanded widget modes

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify the Chat history icon and panel function identically in both the compact (floating) widget and the expanded (full) view.

**Coverage:**
- History icon present in compact mode
- History icon present in expanded mode
- Panel opens and lists sessions in both modes

## Preconditions

- Logged in on {{base_url}}
- At least 1 past support session exists

## Test Data

- Support Assistant widget in default compact position
- Expand button selector: button[aria-label="Expand chat"]

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Support Assistant widget (compact mode) | Widget opens in floating mode |
| 2 | Click 'Chat history' (🕐) icon | History panel opens with session list |
| 3 | Close history panel | Returns to current chat view |
| 4 | Click 'Expand chat' button (aria-label='Expand chat') | Widget expands to full/enlarged view |
| 5 | Click 'Chat history' (🕐) icon in expanded mode | History panel opens with the same session list |
| 6 | Select a session from history | Session messages load correctly within the expanded view |

## Expected Final State

Session messages load correctly within the expanded view

## Pass/Fail Criteria

**Pass:**
- History icon visible and functional in both modes
- Same session list shown in both modes

**Fail:**
- History icon missing or non-functional in one mode
- History panel behaves differently between modes
