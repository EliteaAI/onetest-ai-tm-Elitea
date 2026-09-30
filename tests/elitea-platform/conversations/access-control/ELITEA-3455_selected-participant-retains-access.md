---
id: ELITEA-3455
title: "Selected Participant Retains Access After Restrict"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, permission, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-3455: Selected Participant Retains Access After Restrict

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that participants who are explicitly selected in the Restrict Access wizard retain full access to the conversation.

## Preconditions

- A PUBLIC conversation exists accessible by User A (author), User B, User C, User D
- User A is logged in to {{base_url}} as author

## Test Data

| Field | Value |
|-------|-------|
| User A | Conversation Author |
| User B | Participant to retain |
| User C, D | Participants to remove |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, open Restrict Access wizard | All 4 participants displayed |
| 2 | Remove User C and User D (click x) | C and D removed from selection |
| 3 | Verify User B remains selected | User B chip still present |
| 4 | Click "Restrict access" button | Restriction applied |
| 5 | Login as User B | Login successful |
| 6 | Navigate to Chats | Chat list displayed |
| 7 | Locate the conversation | Conversation IS visible in list |
| 8 | Click to open conversation | Conversation opens successfully |
| 9 | View message history | All messages visible |
| 10 | Send a new message | Message sends (if user has send permission) |
| 11 | Refresh page | Conversation still accessible |
| 12 | Verify via direct link | Direct URL works |

## Expected Final State

- Selected participant (User B) has full access
- Unselected participants (C, D) lost access
- Access persists after page refresh

## Teardown

- None required
