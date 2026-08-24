---
id: ELITEA-2634
title: "Change Duplicate Visibility - Original Visibility Unaffected"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
automation_test_id: []
tags: [chat, duplicate, visibility, independence, P1]
requirements: [3837]
---
# ELITEA-2634: Change Duplicate Visibility - Original Visibility Unaffected

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that changing the visibility of the duplicated chat (making it public or private) does not affect the original chat's visibility status.

## Preconditions

- User is logged in to {{base_url}}
- Team project context
- Original chat exists (can be public or private)
- Duplicate of the chat created
- User has permission to manage chat visibility

## Test Data

- URL: {{base_url}}
- Team project
- Original chat (note initial visibility state)
- Duplicated chat

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Document original chat's visibility status | Note: Public (green) or Private (no green) |
| 2 | Duplicate the chat | Duplicate created with same visibility |
| 3 | Verify duplicate has same initial visibility | Duplicate matches original visibility |
| 4 | Change duplicated chat visibility (e.g., make public if private, or make private if public) | Duplicate visibility changed successfully |
| 5 | Verify duplicate now has new visibility indicator | Green indicator appears/disappears accordingly |
| 6 | Navigate to original chat in chat list | Original chat visible |
| 7 | Verify original chat visibility is UNCHANGED | Original retains initial visibility status |
| 8 | Open original chat and check properties | Original visibility confirmed unchanged |
| 9 | Log in as non-participant (if applicable) | Different user logs in |
| 10 | Verify non-participant access matches original visibility | Original visibility rules still apply |

## Expected Final State

- Duplicate visibility changed as requested
- Original visibility unchanged
- Both chats independent in visibility control
- No cross-chat visibility impact

## Pass/Fail Criteria

**Pass:**
- Duplicate visibility changes successfully
- Original visibility remains unchanged
- Green indicator on original unaffected
- Chats maintain independent visibility states
- No synchronization or coupling

**Fail:**
- Original visibility changes when duplicate changes
- Green indicator on original affected
- Visibility states synchronized
- Changes propagate between chats
- Independence violated
