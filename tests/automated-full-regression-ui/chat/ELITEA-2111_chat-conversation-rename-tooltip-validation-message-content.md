---
id: ELITEA-2111
title: "Chat – Conversation Rename – Tooltip Validation Message Content"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: "tests.ui.chat.test_conversation_rename_invalid_chars_and_recovery.TestConversationRenameInvalidCharsAndRecovery.test_rename_checkmark_inactive_for_invalid_input_shows_tooltip[ELITEA-2111-dollar-percent-at-characters]"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1522
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2111: Chat – Conversation Rename – Tooltip Validation Message Content

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that the tooltip displayed when hovering over the inactive checkmark icon during rename shows the exact required validation message text.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| Invalid name | name with $ % @ characters |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over a conversation, click three-dot icon, click Edit | Conversation name is editable |
| 2 | Clear the current name and type an invalid name (e.g. containing $ % @ or other unsupported characters) then hover over inactive check icon | Tooltip appears near the input field |
| 3 | Verify the tooltip text reads: "The chat name should be 3 to 64 characters long. It can include letters (a-z, A-Z), numbers (0-9), underscores (_), brackets ([]), parentheses (()), dots (.), hyphen(-), and spaces. Please note that the first character should not be a space." | Tooltip shows exact expected text |
| 4 | Verify the checkmark icon remains inactive while invalid characters are present | Checkmark stays inactive |
| 5 | Remove the invalid characters and replace with a valid name of at least 3 characters | Tooltip disappears; checkmark becomes active |

---

## Expected Final State

The validation tooltip shows the exact required message text; removing invalid characters makes the checkmark active.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Tooltip text matches exactly; checkmark activates after valid input.

**Fail:**
- Any step produces an error or unexpected result.
- Tooltip text is wrong, missing, or checkmark remains inactive after valid input.
