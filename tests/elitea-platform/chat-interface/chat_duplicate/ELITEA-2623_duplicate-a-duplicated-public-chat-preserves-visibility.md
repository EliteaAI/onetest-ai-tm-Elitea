---
id: ELITEA-2623
title: "Duplicate a Duplicated Public Chat Preserves Public Visibility"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
automation_test_id: []
tags: [chat, duplicate, public, nested-duplication, P0]
requirements: [3837]
---
# ELITEA-2623: Duplicate a Duplicated Public Chat Preserves Public Visibility

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that duplicating a chat that is itself a duplicate of a public chat preserves the public visibility status through multiple levels of duplication.

## Preconditions

- User is logged in to {{base_url}} in a team project
- Original public chat exists (green indicator)
- First duplicate of the public chat has been created

## Test Data

- URL: {{base_url}}
- Team project
- Original public chat (green)
- First duplicate (green)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify the original public chat has green indicator | Original is public (green marked) |
| 2 | Duplicate the original public chat (create first duplicate) | First duplicate created with green indicator |
| 3 | Verify the first duplicate has green public indicator | First duplicate is public (green) |
| 4 | Duplicate the first duplicate chat (create second duplicate) | Second duplicate created successfully |
| 5 | Verify the second duplicate also has green public indicator | Second duplicate is public (green) |
| 6 | Verify all three chats are visible in the chat list | Original, first duplicate, and second duplicate all visible |
| 7 | Check that all three chats have green indicators | All three chats marked as public |
| 8 | Log in as a non-participant team member | Different user logs in |
| 9 | Verify all three chats are visible to the non-participant | All public chats visible regardless of participant status |

## Expected Final State

- Original public chat remains public (green)
- First duplicate is public (green)
- Second duplicate (duplicate of duplicate) is also public (green)
- Public visibility state propagates through multiple duplication levels
- All team members can see all three chats

## Pass/Fail Criteria

**Pass:**
- All chats (original, 1st duplicate, 2nd duplicate) have green indicators
- Public visibility preserved through nested duplication
- All team members can see all public chats
- No visibility degradation occurs

**Fail:**
- Second duplicate loses public status
- Green indicator missing on any duplicate
- Visibility restricted after nested duplication
- Non-participants cannot see nested duplicates
