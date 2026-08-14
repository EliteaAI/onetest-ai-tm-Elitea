---
id: ELITEA-2110
title: "Chat – Conversation Rename – Check Icon Inactive When Name Contains Special Characters"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: "tests.ui.chat.test_conversation_rename_invalid_chars_and_recovery.TestConversationRenameInvalidCharsAndRecovery.test_rename_checkmark_inactive_for_invalid_input_shows_tooltip[ELITEA-2110-special-characters]"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1522
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2110: Chat – Conversation Rename – Check Icon Inactive When Name Contains Special Characters

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that entering unsupported special characters disables the checkmark icon and shows a validation tooltip.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| Invalid name | HI Chat$$% |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over a conversation, click three-dot icon, click Edit | Conversation name is editable |
| 2 | Clear the current name and type 'HI Chat$$%' then hover over the inactive check icon | Tooltip or hint message appears |
| 3 | Verify the tooltip text indicates allowed characters: 3 to 64 chars, letters, numbers, underscores, brackets, parentheses, dots, hyphens, spaces; first char not a space | Tooltip shows correct validation message |
| 4 | Verify the checkmark icon is in a disabled/inactive state | Checkmark inactive |
| 5 | Attempt to click the checkmark icon | Click has no effect |
| 6 | Verify the conversation name remains unchanged | Name unchanged |

---

## Expected Final State

Checkmark is disabled for invalid characters and tooltip shows the validation rules.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Checkmark inactive for invalid chars; tooltip shows validation message.

**Fail:**
- Any step produces an error or unexpected result.
- Checkmark active for invalid chars or tooltip not shown.
