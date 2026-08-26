---
id: ELITEA-2822
title: "Chat – Switching Suggestion Chips Replaces Unedited Input Text, but Never Overwrites User Edits"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6254]
requirements: [EliteaAI/elitea_issues#6254]
---

# ELITEA-2822: Chat – Switching Suggestion Chips Replaces Unedited Input Text, but Never Overwrites User Edits

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify selecting a different chip while the input still holds the previous suggestion unedited replaces the input text, but once the user has manually edited the inserted text (even one character), selecting another chip does not overwrite it. Also verify clearing the input manually then selecting a chip inserts normally.

---

## Preconditions

- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- A suggestion-eligible AI response has rendered at least 2 chips.

---

## Test Data

| Field | Value |
|-------|-------|
| Chip 1, Chip 2 | Two distinct rendered suggestion chips |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Click Chip 1 | Chip 1's text is inserted into the input |
| 2 | Without editing the input, click Chip 2 | Input text is replaced entirely by Chip 2's text |
| 3 | Click Chip 1 again, then manually edit one character of the inserted text | Input now holds the edited text |
| 4 | Click Chip 2 | Input text is NOT overwritten; the user's edited text remains |
| 5 | Manually clear the input completely, then click Chip 1 | Chip 1's text is inserted normally into the now-empty input |

---

## Expected Final State

Chip selection only auto-replaces input text that still exactly matches a previously-inserted, unedited suggestion; any user edit "locks in" the text against further chip-driven overwrites.

---

## Pass/Fail Criteria

**Pass:**
- Switching chips before any edit replaces the text as expected.
- Switching chips after an edit leaves the edited text untouched.
- Clearing the input then clicking a chip inserts text normally.

**Fail:**
- A chip click overwrites text the user has manually edited.
- A chip click fails to replace unedited previously-inserted suggestion text.
