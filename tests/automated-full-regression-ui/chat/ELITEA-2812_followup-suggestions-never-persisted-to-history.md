---
id: ELITEA-2812
title: "Chat – Follow-Up Suggestions Are Never Persisted to Database or Conversation History"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6123, issue:6254]
requirements: [EliteaAI/elitea_issues#6123, EliteaAI/elitea_issues#6254]
---

# ELITEA-2812: Chat – Follow-Up Suggestions Are Never Persisted to Database or Conversation History

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify follow-up suggestion chips are transient client-side state only — never written to the conversation's persisted history or database, and never reappear after a reload.

---

## Preconditions

- User is logged in to the Elitea platform.
- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- User has an open conversation with at least one AI response that produced suggestion chips.

---

## Test Data

| Field | Value |
|-------|-------|
| Message | Any prompt that produces a suggestion-eligible AI response |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Send the message and wait for the suggestion chip list to render | Chips render above the composer |
| 2 | Inspect the conversation persistence API call/payload made when the AI response was saved | Suggestion text is absent from the persisted message payload |
| 3 | Reload the Chat page | Chip list from before reload does not reappear |
| 4 | Close and reopen the same conversation (navigate away and back) | Chip list does not reappear |
| 5 | Open the same conversation in a second browser tab | Chip list is absent in the second tab |

---

## Expected Final State

Suggestion chips exist only in the live client state of the tab that generated them and disappear permanently on reload, reopen, or in any other tab/session.

---

## Pass/Fail Criteria

**Pass:**
- No suggestion data appears in the persisted conversation payload.
- Chips never reappear after reload, reopen, or in another tab.

**Fail:**
- Suggestion text is found in the persisted payload/history.
- Chips reappear after a reload or in another tab/session viewing the same conversation.
