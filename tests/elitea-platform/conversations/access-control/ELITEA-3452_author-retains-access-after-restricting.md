---
id: ELITEA-3452
title: "Author Retains Full Access After Restricting Conversation"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, permission, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-3452: Author Retains Full Access After Restricting Conversation

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the conversation author retains full access to the conversation after restricting it.

## Preconditions

- Logged in to {{base_url}} as conversation creator/author
- A PUBLIC conversation exists with 5+ participants
- Conversation has message history

## Test Data

| Field | Value |
|-------|-------|
| User Role | Conversation Author |
| Participants | 5+ users + AI agents |
| Message History | Existing messages |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Restrict Access wizard | Wizard displays all participants |
| 2 | Remove all users except author | Only author chip remains |
| 3 | Remove all AI participants | AI section empty |
| 4 | Click "Restrict access" button | Restriction applied, wizard closes |
| 5 | Verify conversation is accessible | Conversation opens normally |
| 6 | View all messages | All message history visible |
| 7 | Send a new message | Message sends successfully |
| 8 | Access conversation settings | Full settings access available |
| 9 | Open action dropdown | All author actions available |
| 10 | Verify "Make public" option visible | Can re-make conversation public |
| 11 | Refresh page | Conversation still accessible |
| 12 | Logout and login again | Conversation still accessible to author |

## Expected Final State

- Author has unrestricted access to their conversation
- All author capabilities preserved
- Can manage conversation normally

## Teardown

- None required
