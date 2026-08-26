---
id: ELITEA-2821
title: "Chat – Clicking a Follow-Up Suggestion Chip Inserts Editable Text Without Sending"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6254]
requirements: [EliteaAI/elitea_issues#6254]
---

# ELITEA-2821: Chat – Clicking a Follow-Up Suggestion Chip Inserts Editable Text Without Sending

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify clicking a suggestion chip inserts its full text into the Chat input as editable content, does not send the message, and moves focus to the input.

---

## Preconditions

- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- A suggestion-eligible AI response has rendered a chip list.

---

## Test Data

| Field | Value |
|-------|-------|
| Chip | Any rendered suggestion chip |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Click one of the rendered chips | The chip's full text is inserted into the Chat input |
| 2 | Observe whether the message was sent | No message was sent; the conversation is unchanged aside from the composer text |
| 3 | Attempt to edit the inserted text in the input (add/remove characters) | Text is fully editable, as if manually typed |
| 4 | Check where keyboard focus is immediately after the click | Focus is on the Chat input |

---

## Expected Final State

Clicking a chip behaves purely as a text-insertion convenience — no send occurs, and the resulting text is normal editable input content with focus on the composer.

---

## Pass/Fail Criteria

**Pass:**
- Chip text is inserted verbatim and is editable.
- No message is sent as a result of the click.
- Focus moves to the Chat input after the click.

**Fail:**
- Clicking a chip sends the message.
- Inserted text is not editable or does not match the chip's full text.
- Focus does not move to the input.
