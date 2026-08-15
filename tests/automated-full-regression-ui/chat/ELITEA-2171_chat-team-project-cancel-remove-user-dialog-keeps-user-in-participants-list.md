---
id: ELITEA-2171
title: "Chat – Team Project – Cancel Remove User Dialog Keeps User in Participants List"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_team_users_mention_and_remove_participants.TestTeamUsersMentionAndRemoveParticipants.test_team_users_mention_and_remove_participants
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1561
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2171: Chat – Team Project – Cancel Remove User Dialog Keeps User in Participants List

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking Cancel in the Remove User dialog preserves the user in the participants list.

---

## Preconditions

- User is logged in to the Elitea platform.
- A conversation with at least 2 participants exists in a Team project.

---

## Test Data

| Field | Value |
|-------|-------|
| User | user_1 |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Open the conversation, click avatar group, hover over user_1, click trash bin | 'Remove user?' modal appears |
| 2 | Click Cancel | Modal closes without removing user |
| 3 | Verify user_1 still listed in USERS dropdown and PARTICIPANTS | user_1 still present |

---

## Expected Final State

User not removed after cancelling.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Cancel preserves user in list.

**Fail:**
- Any step produces an error or unexpected result.
- User removed despite cancelling.
