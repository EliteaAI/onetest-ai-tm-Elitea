---
id: ELITEA-2113
title: "Chat – Conversation Rename – Valid Characters Are Accepted and Saved after invalid values are deleted"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2113: Chat – Conversation Rename – Valid Characters Are Accepted and Saved after invalid values are deleted

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that after typing invalid characters (making the checkmark inactive), replacing them with valid characters enables the checkmark and allows saving.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| Valid name | Chat 01 (test). |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over a conversation, click three-dot icon, click Edit | Conversation name is editable |
| 2 | Clear the current name and type invalid characters | Checkmark is inactive |
| 3 | Clear the invalid input and type "Chat 01 (test)." | Checkmark icon becomes active; no validation error shown |
| 4 | Click the checkmark icon | Conversation is renamed to "Chat 01 (test)." in the left panel |
| 5 | Verify no error message is shown | Rename applied successfully |

---

## Expected Final State

After replacing invalid characters with valid ones, the checkmark becomes active and the rename succeeds.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Valid characters accepted; rename succeeds with "Chat 01 (test).".

**Fail:**
- Any step produces an error or unexpected result.
- Valid characters not accepted or rename fails.
