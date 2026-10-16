---
id: ELITEA-2632
title: "Duplicated Public Chat Displays Green Public Indicator"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [chat, duplicate, public, green-indicator, P1]
requirements: [3837]
---
# ELITEA-2632: Duplicated Public Chat Displays Green Public Indicator

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the duplicated public chat displays the same green user/public indicator as the original, confirming public status inheritance.

## Preconditions

- User is logged in to {{base_url}}
- Team project context
- Original public chat exists with green indicator
- Duplicate of public chat created

## Test Data

- URL: {{base_url}}
- Team project
- Original public chat (green indicator)
- Duplicated public chat

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Locate original public chat in chat list | Original chat visible with green indicator |
| 2 | Duplicate the public chat | Duplicate created successfully |
| 3 | Locate duplicated chat in chat list | Duplicated chat appears in list |
| 4 | Verify duplicated chat has green indicator | Green indicator visible on duplicate |
| 5 | Compare green indicators on both chats | Both have same green color/marker |
| 6 | Open duplicated chat | Duplicated chat opens |
| 7 | Verify public status in chat properties | Duplicate marked as public |
| 8 | Check that duplicate appears in public chat listings | Duplicate in public scope |

## Expected Final State

- Duplicated chat has green public indicator
- Green indicator matches original chat's indicator
- Public status visibly inherited
- Both chats identifiable as public

## Pass/Fail Criteria

**Pass:**
- Duplicated chat has green indicator
- Green indicator matches original
- Public status clearly inherited
- Visual consistency between original and duplicate
- Both marked as public

**Fail:**
- Duplicate lacks green indicator
- Indicator different from original
- Public status not inherited
- Visual inconsistency
- Duplicate appears non-public
