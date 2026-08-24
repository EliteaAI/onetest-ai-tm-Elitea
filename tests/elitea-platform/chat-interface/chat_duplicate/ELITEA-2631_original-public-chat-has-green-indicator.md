---
id: ELITEA-2631
title: "Original Public Chat Displays Green Public Indicator"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
automation_test_id: []
tags: [chat, duplicate, public, green-indicator, P1]
requirements: [3837]
---
# ELITEA-2631: Original Public Chat Displays Green Public Indicator

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the original public chat is visibly marked with the green user/public indicator in the chat list to distinguish it from non-public chats.

## Preconditions

- User is logged in to {{base_url}}
- Team project context
- Public chat exists
- Non-public chat exists for comparison

## Test Data

- URL: {{base_url}}
- Team project
- Public chat (should have green indicator)
- Non-public chat (should not have green indicator)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to chat list in team project | Chat list displays |
| 2 | Locate a public chat in the list | Public chat is visible |
| 3 | Verify the public chat has a green color indicator | Green indicator/marker visible on chat |
| 4 | Locate a non-public chat for comparison | Non-public chat visible |
| 5 | Verify the non-public chat does NOT have green indicator | No green marker on non-public chat |
| 6 | Open the public chat | Public chat opens |
| 7 | Verify public status in chat settings/properties | Chat marked as public/shared |
| 8 | Return to chat list and re-verify green indicator persists | Green indicator still visible |

## Expected Final State

- Public chat clearly marked with green indicator
- Green indicator visible in chat list
- Visual distinction from non-public chats
- Indicator persists across navigation

## Pass/Fail Criteria

**Pass:**
- Public chat has visible green indicator
- Green color/marker clearly distinguishes public chats
- Non-public chats lack green indicator
- Visual indicator consistent and persistent
- Easy identification of public vs non-public

**Fail:**
- No green indicator on public chat
- Indicator missing or unclear
- No visual distinction between public/non-public
- Indicator inconsistent or disappears
