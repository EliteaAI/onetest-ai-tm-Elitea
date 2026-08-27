---
id: ELITEA-2813
title: "Chat – Follow-Up Suggestions Are Scoped Only to the Triggering User's Session"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6123, issue:6254]
requirements: [EliteaAI/elitea_issues#6123, EliteaAI/elitea_issues#6254]
---

# ELITEA-2813: Chat – Follow-Up Suggestions Are Scoped Only to the Triggering User's Session

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify follow-up suggestions generated from User A's message never appear in User B's session, even when both view the same shared conversation.

---

## Preconditions

- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- Two user accounts (User A, User B) both have access to the same shared conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| Message | Any prompt that produces a suggestion-eligible AI response, sent by User A |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | As User A, send the message and wait for the AI response and suggestion chips to render | Chips render in User A's session |
| 2 | As User B, open the same shared conversation in a separate session/browser | User B's session loads the conversation |
| 3 | Observe whether User B sees any suggestion chips above their composer | No suggestion chips are visible to User B |
| 4 | As User B, send their own message and wait for a response | Suggestions (if eligible) generated for User B's own message appear only in User B's session |

---

## Expected Final State

Each user's suggestion chip list is private to the session/tab that triggered it; no cross-user leakage occurs in shared conversations.

---

## Pass/Fail Criteria

**Pass:**
- User B never sees suggestion chips generated from User A's turn.
- Each user only sees suggestions generated from their own triggering message.

**Fail:**
- Suggestion chips from User A's turn are visible in User B's session.
