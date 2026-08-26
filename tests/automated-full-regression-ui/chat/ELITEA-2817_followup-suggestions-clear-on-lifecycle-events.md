---
id: ELITEA-2817
title: "Chat – Follow-Up Suggestion Chip List Clears on All Defined Lifecycle Events"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6123, issue:6254]
requirements: [EliteaAI/elitea_issues#6123, EliteaAI/elitea_issues#6254]
---

# ELITEA-2817: Chat – Follow-Up Suggestion Chip List Clears on All Defined Lifecycle Events

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify the suggestion chip list clears/hides on each of the documented lifecycle events: sending a message, typing a new message before selecting a suggestion, manually editing the inserted suggestion, a new AI response starting, a new AI response completing, and switching conversations.

---

## Preconditions

- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- User has an open conversation with a suggestion-eligible AI response rendered with chips.

---

## Test Data

| Field | Value |
|-------|-------|
| Message | Any prompt that produces a suggestion-eligible AI response |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | With chips rendered, type a new message in the composer without selecting a chip | Chip list clears/hides as soon as typing begins |
| 2 | Repeat with a fresh eligible response; this time send a message without touching the composer manually | Chip list clears once the message is sent |
| 3 | Repeat with a fresh eligible response; click a chip to insert its text, then manually edit one character of the inserted text | Chip list clears/hides once the user edits the inserted text |
| 4 | Repeat with a fresh eligible response; trigger a new AI turn (send another message) | Chip list clears as soon as the new AI response starts streaming |
| 5 | Let the new AI response complete | Prior chip list remains cleared; a new chip list may render for the new response per eligibility rules |
| 6 | With chips rendered, switch to a different conversation and back | Chip list from the original conversation does not persist/reappear incorrectly |

---

## Expected Final State

Every documented lifecycle event reliably clears the chip list, with no stale suggestions surviving any of the transitions above.

---

## Pass/Fail Criteria

**Pass:**
- All six lifecycle events verified in this test correctly clear/hide the chip list.

**Fail:**
- Any lifecycle event leaves a stale chip list visible or selectable.
