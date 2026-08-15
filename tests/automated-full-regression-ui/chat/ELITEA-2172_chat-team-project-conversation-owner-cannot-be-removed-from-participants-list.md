---
id: ELITEA-2172
title: "Chat – Team Project – Conversation Owner Cannot Be Removed from Participants List"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_owner_has_no_remove_control_in_users_dropdown.TestOwnerHasNoRemoveControlInUsersDropdown.test_owner_has_no_remove_control_in_users_dropdown
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1561
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2172: Chat – Team Project – Conversation Owner Cannot Be Removed from Participants List

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that the conversation owner row has no delete/remove control in the USERS dropdown.

---

## Preconditions

- User is logged in to the Elitea platform.
- A conversation with participants including the owner exists.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Open a conversation, click avatar group to open USERS dropdown | Dropdown shows all participants |
| 2 | Identify the conversation owner in the dropdown | Owner identified |
| 3 | Hover over the owner's row | No trash bin icon appears for the owner |
| 4 | Verify owner row has no delete control | No delete control present |
| 5 | Verify all other (non-owner) rows show trash bin on hover | Trash bin visible for non-owners |

---

## Expected Final State

Owner cannot be removed; only non-owner rows have delete controls.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Owner has no delete control; non-owners do.

**Fail:**
- Any step produces an error or unexpected result.
- Owner has a delete control.
