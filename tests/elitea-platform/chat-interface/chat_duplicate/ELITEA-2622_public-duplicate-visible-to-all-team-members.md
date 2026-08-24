---
id: ELITEA-2622
title: "Public Duplicated Chat Visible to All Team Members"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
automation_test_id: []
tags: [chat, duplicate, public, team-visibility, P0]
requirements: [3837]
---
# ELITEA-2622: Public Duplicated Chat Visible to All Team Members

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that a duplicated public chat is visible to all team members, not just the participants, confirming proper public visibility inheritance.

## Preconditions

- Team project with at least 3 users (User A, User B, User C)
- User A is logged in
- Public chat exists with User A and User B as participants
- User C is a team member but NOT a participant in the original chat

## Test Data

- URL: {{base_url}}
- Team project name
- User A (creator), User B (participant), User C (non-participant team member)
- Original public chat (green marked)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | User A: Open the public chat with User B as participant | Public chat opens (green indicator visible) |
| 2 | User A: Verify User C is NOT a participant | User C not in participants panel |
| 3 | User A: Duplicate the public chat | Duplicate created successfully |
| 4 | User A: Verify duplicated chat has green public indicator | Duplicated chat is public (green) |
| 5 | User C: Log in to the same team project | User C successfully logs in |
| 6 | User C: Navigate to the chat list | Chat list displays |
| 7 | User C: Verify the original public chat is visible | Original public chat is visible to User C |
| 8 | User C: Verify the duplicated public chat is also visible | Duplicated public chat is visible to User C |
| 9 | User C: Open the duplicated public chat | User C can access duplicated chat despite not being a participant |

## Expected Final State

- Duplicated public chat is visible to all team members
- Non-participant team members (User C) can see and access the duplicated chat
- Green public indicator confirms visibility scope
- Public visibility is properly inherited

## Pass/Fail Criteria

**Pass:**
- User C (non-participant) can see duplicated public chat
- Both original and duplicate have green indicators
- All team members have visibility access
- Public visibility scope is maintained

**Fail:**
- Duplicated chat only visible to participants
- User C cannot see or access duplicated chat
- Green indicator missing
- Visibility restricted to participants only
