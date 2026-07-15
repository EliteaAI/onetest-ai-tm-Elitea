---
id: ELITEA-2108
title: "Chat – Conversation Rename – Check Icon Inactive for 2 Character Input"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2108: Chat – Conversation Rename – Check Icon Inactive for 2 Character Input

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that the checkmark (save) icon remains disabled when exactly 2 characters are entered in the rename field.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| Two characters | AB |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over a conversation, click three-dot icon, click Edit | Conversation name is editable |
| 2 | Clear the current name and type exactly 2 characters ('AB') | 2 characters appear in the field |
| 3 | Verify the checkmark icon remains in a disabled/inactive state | Checkmark is inactive |
| 4 | Attempt to click the checkmark icon | Click has no effect; save is not triggered |

---

## Expected Final State

Checkmark icon stays inactive for 2-character input; save cannot be triggered.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Checkmark inactive for 2-character input.

**Fail:**
- Any step produces an error or unexpected result.
- Save is triggered with 2 characters.
