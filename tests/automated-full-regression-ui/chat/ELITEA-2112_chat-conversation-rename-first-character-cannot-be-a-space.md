---
id: ELITEA-2112
title: "Chat – Conversation Rename – First Character Cannot Be a Space"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2112: Chat – Conversation Rename – First Character Cannot Be a Space

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that a space cannot be used as the first character in the conversation rename field and that the checkmark icon remains inactive in this case.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over a conversation, click three-dot icon, click Edit | Conversation name is editable |
| 2 | Clear the current name and press the Space key as the first character, then enter 2 more valid characters | Space is not accepted as the first valid character |
| 3 | Verify the checkmark remains inactive and is not clickable | Checkmark stays inactive |

---

## Expected Final State

A leading space is rejected; the checkmark icon remains inactive when the name starts with a space.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Leading space rejected; checkmark stays inactive.

**Fail:**
- Any step produces an error or unexpected result.
- Leading space is accepted or checkmark becomes active.
