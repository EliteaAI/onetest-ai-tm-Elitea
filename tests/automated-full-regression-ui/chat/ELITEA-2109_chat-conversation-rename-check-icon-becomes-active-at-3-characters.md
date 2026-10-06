---
id: ELITEA-2109
title: "Chat – Conversation Rename – Check Icon Becomes Active at 3 Characters"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2109: Chat – Conversation Rename – Check Icon Becomes Active at 3 Characters

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that the checkmark (save) icon transitions from inactive to active exactly when the input reaches 3 characters.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| Three characters | ABC |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over a conversation, click three-dot icon, click Edit | Conversation name is editable |
| 2 | Clear the current name and type 2 characters ('AB') | Checkmark icon is inactive/greyed out |
| 3 | Type one more character to reach 3 characters ('ABC') | Checkmark icon becomes active/enabled |
| 4 | Click the checkmark icon | Conversation is renamed to 'ABC'; change applied in left panel |

---

## Expected Final State

Checkmark icon activates at exactly 3 characters; conversation is renamed successfully.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Checkmark activates at 3 characters; rename succeeds.

**Fail:**
- Any step produces an error or unexpected result.
- Checkmark does not activate at 3 characters.
