---
id: ELITEA-2819
title: "Chat – Deleting the Source AI or User Message Clears Its Associated Follow-Up Suggestions"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6123, issue:6254]
requirements: [EliteaAI/elitea_issues#6123, EliteaAI/elitea_issues#6254]
---

# ELITEA-2819: Chat – Deleting the Source AI or User Message Clears Its Associated Follow-Up Suggestions

**Module:** chat-interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify deleting the AI message that suggestions were generated from, or deleting the triggering user message, immediately clears/hides the associated chip list with no stale chips left behind.

---

## Preconditions

- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- User has an open conversation with a suggestion-eligible AI response and rendered chips.

---

## Test Data

| Field | Value |
|-------|-------|
| Message | Any prompt that produces a suggestion-eligible AI response |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | With chips rendered for the latest AI response, delete that AI message using the existing delete-message action | Chip list clears/hides immediately |
| 2 | Repeat with a fresh eligible exchange; this time delete the user's own last message (the one that triggered the AI reply) | Chip list tied to that exchange also clears immediately, with no stale chips referencing the deleted turn |

---

## Expected Final State

Deleting either side of the exchange that produced the current suggestions removes the chip list with no orphaned/stale suggestion state.

---

## Pass/Fail Criteria

**Pass:**
- Deleting the AI message clears the associated chip list.
- Deleting the triggering user message also clears the associated chip list.

**Fail:**
- Chips remain visible/selectable after either message is deleted.
