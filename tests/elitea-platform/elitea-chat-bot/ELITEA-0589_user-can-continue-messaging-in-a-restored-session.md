---
id: ELITEA-0589
title: "User can continue messaging in a restored session"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4778]
requirements: [EliteaAI/elitea_issues#4778]
---
# ELITEA-0589: User can continue messaging in a restored session

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that after restoring a past session from history, the user can send new messages and receive responses within that session.

**Coverage:**
- Composer is active after restoring a session
- New messages sent and received successfully
- Messages sent in the context of the restored session

## Preconditions

- Logged in on {{base_url}}
- A past session with at least 2 messages exists

## Test Data

- Restored session: known session with message "Original question about toolkits"
- New message to send: "Can you elaborate on that?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open history and click the session 'Original question about toolkits' | Session messages are displayed in the widget |
| 2 | Observe the message composer | Input area is active and editable (not disabled or locked) |
| 3 | Type 'Can you elaborate on that?' and send | Message is submitted |
| 4 | Wait for response | Assistant responds within this session |
| 5 | Verify message is appended below existing messages | New message appears at the bottom of the thread after original messages |

## Expected Final State

New message appears at the bottom of the thread after original messages

## Pass/Fail Criteria

**Pass:**
- Composer is active in a restored session
- New message sent and response received

**Fail:**
- Composer is disabled/read-only in restored session
- Message sends to a different session
- No response received
