---
id: ELITEA-0640
title: "Two separate sessions are fully isolated — messages do not cross between them"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [session-isolation, regression, R-2.0.3]
requirements: [EliteaAI/elitea_issues#4775]
---
# ELITEA-0640: Two separate sessions are fully isolated — messages do not cross between them

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Messages sent in session 2 must never appear when the user returns to session 1, and vice versa. Session contamination is a correctness defect — if a user's support history shows messages they did not write, it is also a potential privacy issue.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- Support Assistant panel is open with at least one message already in the current session

## Test Data

- Session 1 message: "First session — question about agents"
- Session 2 message: "Second session — question about pipelines"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send "First session — question about agents" and wait for the response. | Session 1 contains this exchange. |
| 2 | Click the New Chat button to start session 2. | A clean new session opens with the welcome message. Session 1 messages are not visible. |
| 3 | Send "Second session — question about pipelines" and wait for the response. | Session 2 contains this exchange. Session 1 is untouched. |
| 4 | Open Chat History and click on session 1. | Session 1 loads. |
| 5 | Verify that session 1 shows "First session — question about agents" and its response only. | "Second session — question about pipelines" does NOT appear in session 1. |
| 6 | Click New Chat, then open Chat History and click on session 2. | Session 2 loads. |
| 7 | Verify that session 2 shows "Second session — question about pipelines" and its response only. | "First session — question about agents" does NOT appear in session 2. |

## Expected Final State

"First session — question about agents" does NOT appear in session 2.

## Pass/Fail Criteria

Pass:
- Each session contains only its own messages when loaded from history
- No messages cross between sessions

Fail:
- Messages from session 2 appear when loading session 1
- Messages from session 1 appear when loading session 2
- Any mixed or merged conversation content between sessions
