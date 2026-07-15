---
id: ELITEA-2105
title: "Chat – Conversation Rename – Check Icon Inactive When No Changes Made"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2105: Chat – Conversation Rename – Check Icon Inactive When No Changes Made

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that the checkmark (save) icon is disabled when no changes are made to the conversation name in the edit field.

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
| 1 | Navigate to Chats, hover over a conversation, click three-dot icon, click Edit | Conversation name is editable with current name pre-filled |
| 2 | Do not make any changes to the name | Name is unchanged in the input field |
| 3 | Verify the checkmark icon is displayed in a disabled/inactive state (greyed out) | Checkmark is inactive |
| 4 | Attempt to click the checkmark icon | Click has no effect; input remains open without saving |
| 5 | Verify the conversation name remains unchanged | Name unchanged in left panel |

---

## Expected Final State

The checkmark icon is disabled when no changes are made; clicking it has no effect.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Checkmark inactive with no changes; clicking has no effect.

**Fail:**
- Any step produces an error or unexpected result.
- Save is triggered without any changes.
