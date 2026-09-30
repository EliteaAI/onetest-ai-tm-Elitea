---
id: ELITEA-3453
title: "Remove All User Participants Bulk Action Keeps Author"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, bulk-action, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-3453: Remove All User Participants Bulk Action Keeps Author

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "Remove all user participants" bulk action removes all users except the author.

## Preconditions

- Logged in to {{base_url}} as conversation creator/author
- A PUBLIC conversation exists with 5+ user participants
- Restrict Access wizard is open

## Test Data

| Field | Value |
|-------|-------|
| User Role | Conversation Author |
| User Participants | 5+ users including author |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Restrict Access wizard | Wizard displays |
| 2 | Count user participant chips | 5+ users displayed in "User participants" section |
| 3 | Note which chip is the author | Author chip identified |
| 4 | Locate "Remove all user participants" action | Button/link is visible |
| 5 | Click "Remove all user participants" | Bulk removal triggered |
| 6 | Verify author chip status | Author chip REMAINS selected |
| 7 | Verify other user chips | All non-author user chips are REMOVED/deselected |
| 8 | Count remaining user chips | Only 1 chip remains (author) |
| 9 | Click "Restrict access" to confirm | Operation succeeds |
| 10 | Login as one of the removed users | User CANNOT access conversation |

## Expected Final State

- Only author has access after bulk remove
- Removed users lost access immediately
- Author chip cannot be bulk-removed

## Teardown

- None required
