---
id: ELITEA-2654
title: "Send mid-turn message while agent is running and verify toggle controls feature"
priority: critical
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:chat, eng:backend, eng:frontend, eng:sdk, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has an active chat conversation

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Initial prompt | "Write a detailed 500-word essay about climate change" |
| Mid-turn message | "Focus more on renewable energy solutions" |

## Scenario 1: Mid-turn Input Enabled

### Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings > General > Chat section | Chat settings visible |
| 2 | Enable Mid-turn Input (Beta) toggle | Toggle switches to ON |
| 3 | Navigate to Chat and open a conversation | Chat interface loads |
| 4 | Send a message that triggers a long-running agent response | Agent starts processing, streaming indicator visible |
| 5 | While the agent is still generating, type a message in the input field | Input field accepts text while agent is running |
| 6 | Click Send or press Enter to send the mid-turn message | Message is sent |
| 7 | Observe the UI feedback | Message appears with "sent while running" indicator |
| 8 | Verify agent processes the mid-turn input | Agent response adjusts based on mid-turn instruction |

## Scenario 2: Mid-turn Input Disabled

### Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 9 | Navigate to Settings > General > Chat section | Chat settings visible |
| 10 | Disable Mid-turn Input (Beta) toggle | Toggle switches to OFF |
| 11 | Navigate to Chat and open a new conversation | Chat interface loads |
| 12 | Send a message to trigger a long-running agent response | Agent starts processing |
| 13 | While agent is generating, attempt to type in the input field | Input field is disabled or unavailable |
| 14 | Attempt to click/focus the input field | Input field does not accept focus or text |

## Expected Final State

**Scenario 1:** Mid-turn message is accepted, displayed with indicator, and processed by the agent.

**Scenario 2:** Input field remains disabled during agent execution, maintaining existing behavior when toggle is OFF.

## Pass/Fail Criteria

**Pass:**
- **When toggle ON:** Input field enabled during agent execution, mid-turn message sent and processed, "sent while running" indicator visible
- **When toggle OFF:** Input field disabled during agent execution, user cannot send mid-turn messages, existing behavior preserved

**Fail:**
- Input field behavior doesn't match toggle state
- Mid-turn messages not processed when feature enabled
- Input field enabled when feature disabled
