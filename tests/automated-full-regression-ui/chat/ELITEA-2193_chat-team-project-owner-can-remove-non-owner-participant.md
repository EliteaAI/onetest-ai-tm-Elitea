---
id: ELITEA-2193
title: "Chat – Team Project – Owner Can Remove Non-Owner Participant via Confirm Dialog"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_team_users_mention_and_remove_participants.TestTeamUsersMentionAndRemoveParticipants.test_team_users_mention_and_remove_participants
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1566
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2193: Chat – Team Project – Owner Can Remove Non-Owner Participant via Confirm Dialog

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that the conversation owner can remove a non-owner participant via the confirm dialog.

---

## Preconditions

- User is logged in to the Elitea platform.
- Logged in as conversation owner in a Team project with multiple participants.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Open a conversation where current user is owner | Conversation open |
| 2 | Click avatar group to open USERS dropdown | Dropdown shows all participants |
| 3 | Hover over a non-owner; verify trash bin with 'Remove user' tooltip | Trash bin visible |
| 4 | Click trash bin | 'Remove user?' modal with orange warning icon appears |
| 5 | Verify modal body: 'Are you sure to remove the user from chat?' | Modal text correct |
| 6 | Click Remove | Modal closes; user removed from dropdown and PARTICIPANTS |

---

## Expected Final State

Non-owner participant removed by owner via confirm dialog.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Owner can remove non-owner.

**Fail:**
- Any step produces an error or unexpected result.
- Owner cannot remove non-owner.
