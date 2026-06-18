---
id: ELITEA-0613
title: "Support Assistant conversations are user-specific — User-A cannot see User-B's sessions"
priority: critical
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [session-isolation, multi-user, story:4776, r-2.0.3, privacy]
requirements: [4776, 4773]
---
# ELITEA-0613: Support Assistant conversations are user-specific — User-A cannot see User-B's sessions

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that each user's Support Assistant conversation history is completely private. User-A must only see their own sessions in history. User-B's sessions must not appear in User-A's history, and vice versa. This is both a functional correctness and a security/privacy requirement.

## Preconditions

Two regular user accounts: User-A and User-B.
Both users have sent at least one message in separate Support Assistant sessions.

## Test Data

User-A message: "User A question"
User-B message: "User B question"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User-A, open Support Assistant, send "User A question" | Response received; session exists |
| 2 | Open history view in the Support Assistant | Only User-A's sessions are listed |
| 3 | Log out; log in as User-B, open Support Assistant, send "User B question" | Response received; session exists |
| 4 | Open history view in the Support Assistant as User-B | Only User-B's sessions are listed; "User A question" session does NOT appear |
| 5 | Log out; log back in as User-A |  |
| 6 | Open Support Assistant history as User-A | Only User-A's sessions are listed; "User B question" session does NOT appear |

## Expected Final State

Only User-A's sessions are listed; "User B question" session does NOT appear

## Pass/Fail Criteria

PASS: Each user sees only their own sessions in history.
FAIL: Any session from User-A appears in User-B's history or vice versa.
