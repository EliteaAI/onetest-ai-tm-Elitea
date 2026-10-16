---
id: ELITEA-2639
title: "Duplicated Chat Appears at Top of List - Most Recent Position (Bug #6271)"
priority: low
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [chat, duplicate, sorting, bug-6271, P2]
requirements: [3837, 6271]
---
# ELITEA-2639: Duplicated Chat Appears at Top of List - Most Recent Position (Bug #6271)

**Module:** Chat Interface · **Priority:** Low · **Type:** Functional

**Objective:** Verify that the duplicated chat appears at the top of the chat list as the most recent chat, fixing Bug #6271 where duplicates were not sorted above the original.

## Preconditions

- User is logged in to {{base_url}}
- Chat list with multiple chats exists
- Original chat exists (can be in "Today" section)

## Test Data

- URL: {{base_url}}
- Original chat in "Today" or "This Week" section

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Note the current chat list order | Document chat positions |
| 2 | Identify original chat position in list | Original chat location noted |
| 3 | Duplicate the chat | Duplicate created successfully |
| 4 | Observe chat list immediately after duplication | Chat list refreshes/updates |
| 5 | Verify duplicated chat appears at the TOP of the list | Duplicate is first in "Today" section |
| 6 | Verify duplicated chat is ABOVE the original chat | Duplicate positioned above original |
| 7 | Verify duplicated chat in "Today" section (most recent) | Correct time-based grouping |
| 8 | Create a new chat after duplication | New chat created |
| 9 | Verify new chat appears above duplicated chat | Ordering by recency maintained |
| 10 | Refresh page and verify sorting persists | Duplicate remains in correct position |

## Expected Final State

- Duplicated chat at top of chat list (most recent)
- Duplicated chat above original chat
- Correct time-based section ("Today")
- Sorting by recency maintained
- Bug #6271 fixed

## Pass/Fail Criteria

**Pass:**
- Duplicate appears at top of list immediately
- Duplicate positioned above original
- Correct section grouping ("Today")
- Sorting persists after refresh
- Bug #6271 resolved

**Fail:**
- Duplicate not at top of list
- Duplicate below original (Bug #6271 not fixed)
- Incorrect section grouping
- Sorting incorrect
- Position changes after refresh
