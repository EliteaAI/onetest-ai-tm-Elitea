---
id: ELITEA-2192
title: "Chat – Team Project – Conversation Owner Cannot Be Removed from Participants"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_owner_has_no_remove_control_in_users_dropdown.TestOwnerHasNoRemoveControlInUsersDropdown.test_owner_has_no_remove_control_in_users_dropdown
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1566
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2192: Chat – Team Project – Conversation Owner Cannot Be Removed from Participants

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that attempting to remove the conversation owner shows an error toast.

---

## Preconditions

- User is logged in to the Elitea platform.
- A public conversation with multiple participants exists.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Open a public conversation with multiple participants | PARTICIPANTS panel visible |
| 2 | Click avatar group to open USERS dropdown | Dropdown shows all participants |
| 3 | Hover over conversation owner's row | No trash bin icon visible for owner |
| 4 | Attempt to trigger a delete action on the owner row | Red error toast: 'Cannot delete author of the conversation' |
| 5 | Verify owner remains in dropdown | Owner still listed |

---

## Expected Final State

Owner cannot be removed; error toast shown on attempt.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- No delete for owner; error toast shown.

**Fail:**
- Any step produces an error or unexpected result.
- Owner can be removed.
