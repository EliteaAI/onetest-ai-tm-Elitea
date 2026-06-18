---
id: ELITEA-0617
title: "Starting a new chat session preserves the previous session in history"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [history-preservation, session-management, story:4775, new-chat, r-2.0.3]
requirements: [4775]
---
# ELITEA-0617: Starting a new chat session preserves the previous session in history

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a user starts a new support session (via "New Chat" or equivalent), the old session is preserved in chat history and is accessible — it is not deleted. The new session begins clean with a welcome message or empty composer. No messages from the previous session appear in the new one.

## Preconditions

Support Assistant is enabled.
Tester has an active session with at least 2 messages already sent.

## Test Data

Session 1 message: "How do I export an agent?" (ensure a response is received)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm the current session has messages ("How do I export an agent?" + response) | Messages are visible |
| 2 | Click the "New Chat" button (or equivalent action to start a new session) | The conversation area clears; welcome message is shown or composer is empty and ready |
| 3 | Verify no messages from the previous session appear in the new session | The new session area contains only the welcome message or is empty — no "How do I export an agent?" message is present |
| 4 | Navigate to the history/previous sessions view | Previous session is listed (e.g., with title or date) |
| 5 | Click on the previous session | "How do I export an agent?" and its response are loaded correctly |

## Expected Final State

"How do I export an agent?" and its response are loaded correctly

## Pass/Fail Criteria

PASS: Old session in history with all messages; new session is empty; no message crossover.
FAIL: Old session deleted after New Chat; messages from old session appear in new session.
