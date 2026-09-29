---
id: ELITEA-3454
title: "Non-Selected Project Member Loses Access After Restrict"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, permission, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-3454: Non-Selected Project Member Loses Access After Restrict

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that project members who are not selected in the Restrict Access wizard lose all access to the conversation.

## Preconditions

- A PUBLIC conversation exists accessible by User A (author), User B, User C
- User A is logged in to {{base_url}} as author

## Test Data

| Field | Value |
|-------|-------|
| User A | Conversation Author |
| User B | Participant to be removed |
| User C | Participant to retain access |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, open Restrict Access wizard | Wizard shows A, B, C as participants |
| 2 | Click (x) on User B's chip | User B removed from selection |
| 3 | Keep User C selected | User C remains in selection |
| 4 | Click "Restrict access" button | Restriction applied |
| 5 | Logout from User A | Logged out |
| 6 | Login as User B | Login successful |
| 7 | Navigate to Chats sidebar | Chat list displayed |
| 8 | Search for the conversation | Conversation NOT FOUND in results |
| 9 | Check chat list directly | Conversation NOT visible |
| 10 | Try direct URL to conversation | Access DENIED / 403 Forbidden |
| 11 | Logout from User B | Logged out |
| 12 | Login as User C | Login successful |
| 13 | Navigate to conversation | Conversation IS accessible |
| 14 | Open and view messages | Full access confirmed |

## Expected Final State

- User B completely lost access
- User C retained access
- Access changes applied immediately

## Teardown

- None required
