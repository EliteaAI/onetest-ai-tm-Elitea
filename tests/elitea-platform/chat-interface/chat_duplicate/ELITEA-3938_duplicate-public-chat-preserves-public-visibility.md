---
id: ELITEA-3938
title: "Duplicate Public Chat Preserves Public Visibility (Green Indicator)"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [chat, duplicate, public, visibility, P0]
requirements: [3837]
---
# ELITEA-3938: Duplicate Public Chat Preserves Public Visibility (Green Indicator)

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that duplicating a public chat (marked with green indicator) creates a duplicate that is also public with the green visibility indicator.

## Preconditions

- User is logged in to {{base_url}} in a team project
- A public chat exists (marked with green color/indicator)
- User has permission to create and share public chats

## Test Data

- URL: {{base_url}}
- Team project with multiple users
- Existing public chat (green marked)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the chat list in a team project | Chat list displays with team project chats |
| 2 | Identify a public chat (marked with green indicator) | Public chat is visible with green color/icon |
| 3 | Verify the original chat shows the green public indicator | Green indicator confirms public visibility |
| 4 | Duplicate the public chat using the context menu | Duplicate action completes successfully |
| 5 | Locate the duplicated chat in the chat list | Duplicated chat appears in the list |
| 6 | Verify the duplicated chat also has the green public indicator | Duplicated chat is marked as public (green indicator) |
| 7 | Open the duplicated chat | Duplicated chat opens successfully |
| 8 | Verify public status is maintained in chat settings/properties | Chat properties confirm public visibility |

## Expected Final State

- Original public chat retains green indicator
- Duplicated chat is also public with green indicator
- Both chats are visible to all team members
- Public visibility state is inherited

## Pass/Fail Criteria

**Pass:**
- Original chat remains public (green indicator)
- Duplicated chat is also public (green indicator)
- Both chats display green visibility marker
- Public state is correctly inherited

**Fail:**
- Duplicated chat is not public
- Green indicator missing on duplicate
- Visibility state not inherited
- Only participant users can see duplicate (should be visible to all)
