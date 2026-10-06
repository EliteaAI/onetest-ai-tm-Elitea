---
id: ELITEA-2671
title: "Mid-turn Input Happy Path - Enable, Send, Process, History, Persistence"
priority: critical
type: functional
module: default-modules
status: draft
execution_type: manual
tags: [feat:chat, feat:settings, eng:backend, eng:frontend, eng:sdk, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has permission to modify project settings
- Browser: Chrome/Firefox/Edge (latest)

## Test Data

| Field | Value |
|-------|-------|
| Settings URL | `{{base_url}}/app/settings` |
| Chat URL | `{{base_url}}/app/chat` |
| Initial prompt | "Write a detailed 500-word essay about climate change" |
| Mid-turn message | "Focus more on renewable energy solutions" |
| Expected description | "Send a message to an agent while it is still working, to steer the rest of the run." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → General | Settings page loads |
| 2 | Scroll to Chat section | Chat section is visible |
| 3 | Verify "Mid-turn Input (Beta)" toggle is present | Toggle is visible with label "Mid-turn Input (Beta)" |
| 4 | Verify the description text | Description reads: "Send a message to an agent while it is still working, to steer the rest of the run." |
| 5 | Check toggle initial state | Toggle is OFF |
| 6 | Click the toggle to enable it | Toggle switches to ON |
| 7 | Refresh the page | Page reloads |
| 8 | Navigate back to Settings → General → Chat section | Chat section displayed |
| 9 | Verify toggle state persisted | Toggle remains ON |
| 10 | Navigate to Chat | Chat interface loads |
| 11 | Send the initial prompt | Agent starts processing, streaming indicator visible |
| 12 | While agent is still generating, type mid-turn message in input field | Input field accepts text while agent is running |
| 13 | Send the mid-turn message | Message is sent |
| 14 | Observe UI feedback | Message appears with "sent while running" indicator |
| 15 | Wait for agent to complete the turn | Agent completes response |
| 16 | Review agent's response content | Response reflects mid-turn guidance (focuses on renewable energy) |
| 17 | Scroll through conversation history | All messages are visible |
| 18 | Verify original message is displayed | Original prompt is visible |
| 19 | Verify mid-turn message is displayed | Mid-turn message visible with "sent while running" label |
| 20 | Verify message sequence | Messages in correct order: original → mid-turn → agent response |
| 21 | Refresh the page | Page reloads |
| 22 | Wait for conversation to load | Conversation history loads |
| 23 | Verify all messages persist after reload | Original, mid-turn, and response messages all visible |
| 24 | Verify "sent while running" label preserved | Label remains on mid-turn message |
| 25 | Verify message sequence after reload | All messages in correct chronological order |

## Expected Final State

- Mid-turn Input toggle is enabled and persists across reloads
- User successfully sent mid-turn message during agent execution
- Agent processed mid-turn input and adjusted response
- Conversation history shows all messages in correct order
- Mid-turn message has "sent while running" label
- All messages and labels persist after page reload

## Pass/Fail Criteria

**Pass:**
- Toggle enables, persists, and displays correctly
- Input field enabled during agent execution when toggle ON
- Mid-turn message sent successfully with indicator
- Agent response incorporates mid-turn guidance
- Conversation history shows all messages with correct labels
- All state persists after page reload

**Fail:**
- Toggle does not enable or persist
- Input field disabled during agent execution
- Mid-turn message not sent or processed
- Agent ignores mid-turn input
- Messages missing from history or labels incorrect
- State lost after reload
