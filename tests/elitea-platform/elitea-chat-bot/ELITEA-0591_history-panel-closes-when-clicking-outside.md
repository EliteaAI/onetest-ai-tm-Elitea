---
id: ELITEA-0591
title: "History panel closes when clicking outside"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4778]
requirements: [EliteaAI/elitea_issues#4778]
---
# ELITEA-0591: History panel closes when clicking outside

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify the history dropdown/panel closes when the user clicks anywhere outside of it.

**Coverage:**
- Click-outside dismiss behavior
- Widget returns to current chat view after dismiss

## Preconditions

- Logged in on {{base_url}}
- History panel is open

## Test Data

- Click target outside history: chat message area or page background

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Support Assistant and open 'Chat history' panel | History panel/dropdown is visible |
| 2 | Click on the chat message area of the widget (outside the history panel) | History panel closes |
| 3 | Verify widget state | Widget shows the current chat view; no history panel visible |
| 4 | Open history again; click outside on the main page background | History panel closes again |

## Expected Final State

History panel closes again

## Pass/Fail Criteria

**Pass:**
- History panel dismisses on outside click
- Chat view is correctly restored

**Fail:**
- History panel stays open after clicking outside
- Widget freezes or becomes unresponsive
