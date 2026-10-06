---
id: ELITEA-2176
title: "Chat – Team Project – Cancel Add Users Modal After Pre-Selecting Users Does Not Add Anyone"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2176: Chat – Team Project – Cancel Add Users Modal After Pre-Selecting Users Does Not Add Anyone

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking Cancel in the Add Users modal after pre-selecting users does not add any users.

---

## Preconditions

- User is logged in to the Elitea platform.
- User is in a Team project with an existing conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| Users | user_1, user_2 |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Note current participants in PARTICIPANTS USERS section | Current participants noted |
| 2 | Open Invite Users modal, select user_1 and user_2; verify chips | Two chips shown |
| 3 | Click Cancel | Modal closes without saving |
| 4 | Verify PARTICIPANTS USERS shows same participants as before | No new users added |
| 5 | Verify user_1 and user_2 NOT in PARTICIPANTS | user_1 and user_2 not added |

---

## Expected Final State

No users added after cancelling the modal.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Cancel does not add any users.

**Fail:**
- Any step produces an error or unexpected result.
- Users added despite cancelling.
