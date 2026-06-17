---
id: ELITEA-0595
title: "New chat session appears in history and title contains no internal User ID"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4778]
requirements: [EliteaAI/elitea_issues#4778]
---
# ELITEA-0595: New chat session appears in history and title contains no internal User ID

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that starting a new chat session and exchanging at least one message creates a new entry in the history list, and that the entry title does not expose any internal user ID.

**Coverage:**
- New session created via "+ New chat"
- Session persisted in history after first message exchange
- No internal User ID prefix in the newly created session title

## Preconditions

- Logged in on {{base_url}}
- Support Assistant is open with an existing session visible in history

## Test Data

- Message to send: "What is ELITEA?"
- Expected history label: matches first message text or creation timestamp (no "User ID {N} -" prefix)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Support Assistant and note the current number of sessions in history | History shows N sessions |
| 2 | Click '+ New chat' button | A new empty chat session starts |
| 3 | Send the message: 'What is ELITEA?' | Message is sent; assistant responds |
| 4 | Open 'Chat history' panel | History list now shows N+1 sessions |
| 5 | Verify the new session is present | New session entry is visible with a relevant title and/or timestamp |
| 6 | Inspect the title of the newly created session | Title shows only the session name (e.g., 'What is ELITEA?') — no 'User ID {N} -' prefix or any other internal identifier |

## Expected Final State

Title shows only the session name (e.g., 'What is ELITEA?') — no 'User ID {N} -' prefix or any other internal identifier

## Pass/Fail Criteria

**Pass:**
- New session appears in history after first message exchange
- Session title contains no internal User ID prefix

**Fail:**
- New session does not appear in history
- Session title shows "User ID {N} - " or any other internal identifier prefix
