---
id: ELITEA-2261
title: "Clicking a chat mention notification link navigates to the correct conversation"
priority: medium
type: functional
module: settings-notifications
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_notification_link_navigates_to_conversation.TestNotificationChatMentionLinkNavigation.test_chat_mention_link_navigates_to_conversation
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1788"
---

# ELITEA-2261: Clicking a chat mention notification link navigates to the correct conversation

**Module:** settings-notifications · **Priority:** medium · **Type:** functional

**Objective:** Verify that Clicking a chat mention notification link navigates to the correct conversation. Success is confirmed when navigate back — verify the notification is now in read state.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Notifications | Target page/section loads successfully. |
| 2 | Find a notification of type "[User] mentioned you in [Chat link]" | Action completes without error and produces the expected UI state. |
| 3 | Click the Chat link in the notification text | Control responds; expected next state is shown. |
| 4 | Verify the browser navigates to the referenced chat conversation | Condition holds as described. |
| 5 | Verify the chat opens without a "not found" error | Condition holds as described. |
| 6 | Navigate back — verify the notification is now in read state | Target page/section loads successfully. |

---

## Expected Final State

Navigate back — verify the notification is now in read state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Clicking a chat mention notification link navigates to the correct conversation.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
