---
id: ELITEA-0599
title: "Clicking a past session in history loads its full message thread"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4778]
requirements: [EliteaAI/elitea_issues#4778]
---
# ELITEA-0599: Clicking a past session in history loads its full message thread

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that selecting a session from history loads its complete message thread in the widget.

**Coverage:**
- History item is clickable
- Correct session's messages are loaded
- Active state in history list updates to reflect selected session

## Preconditions

- Logged in on {{base_url}}
- At least 2 completed support sessions exist with known message content

## Test Data

- Session A: first message "Hello, I have a question about agents"
- Session B: first message "How do I configure a pipeline?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Support Assistant widget | Widget opens showing current/active chat |
| 2 | Click 'Chat history' (🕐) icon | History panel opens listing all sessions |
| 3 | Click Session A from the list | Widget transitions to Session A's message thread |
| 4 | Observe messages displayed | All messages from Session A are shown in chronological order with correct content |
| 5 | Open history panel again | Session A is marked/highlighted as the currently loaded session |
| 6 | Click Session B | Widget transitions to Session B's thread; Session A messages are no longer displayed |

## Expected Final State

Widget transitions to Session B's thread; Session A messages are no longer displayed

## Pass/Fail Criteria

**Pass:**
- Correct session's messages load on click
- Messages are complete and in order
- Active indicator in history updates correctly

**Fail:**
- Wrong session's messages appear
- Messages are incomplete, missing, or in wrong order
- No visual indication of which session is active
