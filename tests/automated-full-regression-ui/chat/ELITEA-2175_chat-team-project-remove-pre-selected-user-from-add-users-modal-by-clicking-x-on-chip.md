---
id: ELITEA-2175
title: "Chat – Team Project – Remove Pre-Selected User from Add Users Modal by Clicking X on Chip"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_invite_users_add_cancel_close.TestRemovePreselectedUserViaChipX.test_remove_preselected_user_via_chip_x
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1561
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2175: Chat – Team Project – Remove Pre-Selected User from Add Users Modal by Clicking X on Chip

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking the X on a user chip in the Add Users modal removes that user from the selection.

---

## Preconditions

- User is logged in to the Elitea platform.
- User is in a Team project.

---

## Test Data

| Field | Value |
|-------|-------|
| Users | user_1, user_2, user_3 |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Open Invite Users modal, select user_1, user_2, user_3; verify all three chips visible | Three chips shown |
| 2 | Click X on user_2's chip | user_2 chip removed; user_1 and user_3 remain |
| 3 | Click Add | Modal closes; user_1 and user_3 in PARTICIPANTS; user_2 NOT listed |

---

## Expected Final State

user_2 not added after chip removal; user_1 and user_3 added.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Chip removal works; only remaining users added.

**Fail:**
- Any step produces an error or unexpected result.
- All users added despite chip removal.
