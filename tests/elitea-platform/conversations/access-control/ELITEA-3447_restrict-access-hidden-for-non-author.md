---
id: ELITEA-3447
title: "Restrict Access Action Hidden for Non-Author Users"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, permission, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-3447: Restrict Access Action Hidden for Non-Author Users

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "Restrict access" action is only visible to the conversation author, not to other participants.

## Preconditions

- A PUBLIC conversation exists created by User A
- User B is a project member with access to the conversation (NOT the author)
- User B is logged in to {{base_url}}

## Test Data

| Field | Value |
|-------|-------|
| User A | Conversation Author |
| User B | Project member, NOT author |
| Conversation State | Public |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Login as User B (non-author participant) | Login successful |
| 2 | Navigate to Chats | Conversation list displayed |
| 3 | Locate the public conversation created by User A | Conversation visible and accessible |
| 4 | Right-click on the conversation | Action dropdown opens |
| 5 | Review available actions | "Restrict access" is NOT visible |
| 6 | Attempt to access restrict via direct API call | Server returns 403 Forbidden / permission error |
| 7 | Verify conversation state | Access state unchanged |
| 8 | Login as User A (author) | Login successful |
| 9 | Right-click same conversation | "Restrict access" IS visible for author |

## Expected Final State

- Only author can see and use "Restrict access" action
- API properly validates author permission
- Non-author cannot modify access settings

## Teardown

- None required
