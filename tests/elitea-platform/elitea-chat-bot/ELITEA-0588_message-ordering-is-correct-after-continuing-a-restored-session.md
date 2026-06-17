---
id: ELITEA-0588
title: "Message ordering is correct after continuing a restored session"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4778]
requirements: [EliteaAI/elitea_issues#4778]
---
# ELITEA-0588: Message ordering is correct after continuing a restored session

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that when new messages are sent in a restored session, historical messages remain above and new messages appear chronologically at the bottom.

**Coverage:**
- Correct chronological ordering: old messages → new messages
- No interleaving or position errors

## Preconditions

- Logged in on {{base_url}}
- Restored session contains known messages M1 (oldest), M2, M3 (most recent prior)

## Test Data

- Restored session messages: M1 = "First question", M2 = "Follow-up", M3 = "Last message before restore"
- New message: N1 = "New message after restore"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Restore past session from history | M1, M2, M3 shown in order from top to bottom |
| 2 | Send new message N1 | N1 appears below M3 at the bottom of the thread |
| 3 | Scroll through the full thread | Full order is: M1 → M2 → M3 → N1 — no gaps, no interleaving |

## Expected Final State

Full order is: M1 → M2 → M3 → N1 — no gaps, no interleaving

## Pass/Fail Criteria

**Pass:**
- Historical messages appear above new messages
- Strictly chronological order maintained

**Fail:**
- New message inserted between older messages
- Messages appear out of order or duplicated
