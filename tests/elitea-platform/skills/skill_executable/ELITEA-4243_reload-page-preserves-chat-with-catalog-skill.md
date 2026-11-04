---
id: ELITEA-4243
title: Reload preserves chat conversation with Catalog skill participant
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, skill-run, catalog, chat, persistence, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6922]
---
# ELITEA-4243: Reload preserves chat conversation with Catalog skill participant

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that after reloading the page, chat with Catalog skill participant is preserved with all message history intact.

**Coverage:**
- Chat persists after page reload
- Message history preserved
- Skill participant remains attached
- Conversation can continue

## Preconditions

- User is logged in to {{base_url}}
- Chat with Catalog skill participant exists
- At least 2-3 messages exchanged in the chat

## Test Data

- Existing chat with messages:
  - Message 1: "Hello, tell me a joke about crows"
  - Message 2: "That's funny, tell me another one"
- Expected: All messages preserved after reload

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create chat with Catalog skill via Run button | Chat created with skill participant |
| 2 | Send message: "Hello, tell me a joke about crows" | Message sent, skill responds with crow joke |
| 3 | Send follow-up message: "That's funny, tell me another one" | Message sent, skill responds with another joke |
| 4 | Reload the browser page (press F5 or Ctrl+R) | Page reloads successfully, redirects to main page or stays on chat |
| 5 | Navigate to Chats list in left sidebar | Chats list displays |
| 6 | Click on the chat with Catalog skill | Chat opens in main interface |
| 7 | Observe the chat message history | All messages (2 user messages + 2 skill responses) are intact and visible |
| 8 | Verify message order | Messages appear in correct chronological order |
| 9 | Check skill participant in right panel | Skill still appears in SKILLS participant section |
| 10 | Send a new message: "Give me one more" | Message sends successfully, proving conversation can continue |

## Expected Final State

After reload, chat is preserved with all messages intact; skill participant attached; conversation can continue.

## Pass/Fail Criteria

**Pass:** Page reload preserves chat, all messages visible in correct order, skill participant attached, can continue conversation.

**Fail:** Messages lost after reload, chat not found, or skill participant missing.
