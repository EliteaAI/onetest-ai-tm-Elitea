---
id: ELITEA-2170
title: "Chat – Team Project – Remove User from Conversation via Confirm Dialog"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2170: Chat – Team Project – Remove User from Conversation via Confirm Dialog

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that a user can be removed from conversation participants via the USERS dropdown and confirm dialog.

---

## Preconditions

- User is logged in to the Elitea platform.
- A conversation with at least 2 added participants exists in a Team project.

---

## Test Data

| Field | Value |
|-------|-------|
| User to remove | user_1 |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Open the conversation and click avatar group in PARTICIPANTS USERS section | Dropdown shows all participants plus 'All users' |
| 2 | Hover over user_1's row; verify trash bin icon and 'Remove user' tooltip | Trash bin visible |
| 3 | Click the trash bin icon for user_1 | 'Remove user?' modal appears |
| 4 | Verify modal body: 'Are you sure to remove the user_1 user from conversation?' | Modal text correct |
| 5 | Click Remove | Modal closes; user_1 removed from dropdown and PARTICIPANTS |

---

## Expected Final State

User removed via confirm dialog.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- User removed successfully.

**Fail:**
- Any step produces an error or unexpected result.
- User not removed or modal text wrong.
