---
id: ELITEA-2194
title: "Chat – Team Project – Cancel Remove Participant Dialog Keeps User in List"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2194: Chat – Team Project – Cancel Remove Participant Dialog Keeps User in List

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking Cancel in the Remove Participant dialog keeps the user in the participants list.

---

## Preconditions

- User is logged in to the Elitea platform.
- Logged in as conversation owner with multiple participants.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Open USERS dropdown and hover over a non-owner participant, click trash bin | 'Remove user?' modal appears |
| 2 | Click Cancel | Modal closes without removing user |
| 3 | Verify participant still listed in dropdown and PARTICIPANTS section | User still present |

---

## Expected Final State

User preserved after cancelling removal dialog.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Cancel keeps user in participants.

**Fail:**
- Any step produces an error or unexpected result.
- User removed despite cancelling.
