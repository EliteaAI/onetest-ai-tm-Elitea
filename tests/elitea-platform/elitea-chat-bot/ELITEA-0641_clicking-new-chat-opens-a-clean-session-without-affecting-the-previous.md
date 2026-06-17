---
id: ELITEA-0641
title: "Clicking New Chat opens a clean session without affecting the previous one"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [session-management, new-chat, R-2.0.3, smoke]
requirements: [#4775]
---
# ELITEA-0641: Clicking New Chat opens a clean session without affecting the previous one

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Clicking New Chat must start a completely fresh session. The old session must not be deleted — it must move to the Chat History list and remain accessible. No messages from the prior session should appear in the new one.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- Support Assistant panel is open with at least one completed message exchange in the current session

## Test Data

- Existing message in current session: "Hello, this is my first session"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm the current session has at least one message visible. Note the message text. | At least one user message and response are visible in the conversation. |
| 2 | Click the New Chat button (the + icon in the panel header). | The message area clears. |
| 3 | Observe the message area immediately after clicking New Chat. | Only the welcome message is shown. None of the messages from the previous session appear. |
| 4 | Click the Chat History button (clock/history icon in the panel header). | A dropdown or panel listing previous sessions opens. |
| 5 | Look for the previous session in the history list. | The previous session appears as an entry in the list (identified by the first message text or a session name). |
| 6 | Click on the previous session entry in the history list. | The conversation from the previous session loads with all its original messages intact. |

## Expected Final State

The conversation from the previous session loads with all its original messages intact.

## Pass/Fail Criteria

Pass:
- New Chat opens a clean session with only the welcome message
- No messages from the previous session appear in the new session
- Previous session is preserved in Chat History and accessible with all its messages

Fail:
- Messages from the previous session bleed into the new session
- The previous session is deleted (not present in history)
- New Chat has no visible effect
- Welcome message is not shown in the new session
