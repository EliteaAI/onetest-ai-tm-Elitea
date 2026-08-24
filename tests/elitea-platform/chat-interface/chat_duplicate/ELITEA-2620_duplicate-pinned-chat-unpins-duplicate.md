---
id: ELITEA-2620
title: "Duplicate Pinned Chat - Duplicate is Unpinned, Original Remains Pinned"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
automation_test_id: []
tags: [chat, duplicate, pinned, P0]
requirements: [3837]
---
# ELITEA-2620: Duplicate Pinned Chat - Duplicate is Unpinned, Original Remains Pinned

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that duplicating a pinned chat creates an unpinned duplicate while the original chat remains pinned.

## Preconditions

- User is logged in to {{base_url}}
- An existing chat exists that can be pinned
- User has permission to pin/unpin chats

## Test Data

- URL: {{base_url}}
- Test chat for pinning and duplication

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select an existing chat from the chat list | Chat is selected |
| 2 | Pin the chat using the context menu "Pin on top" option | Chat is pinned and appears at the top of the chat list |
| 3 | Verify the pinned indicator is visible on the original chat | Pin icon or indicator is displayed |
| 4 | Duplicate the pinned chat using the "Duplicate" option | Duplicate action completes successfully |
| 5 | Verify the duplicated chat appears in the chat list | Duplicated chat is visible |
| 6 | Check if the duplicated chat has a pin indicator | Duplicated chat does NOT have a pin indicator (unpinned) |
| 7 | Verify the original chat still shows the pin indicator | Original chat remains pinned at the top |
| 8 | Verify the duplicated chat is in the regular (unpinned) section | Duplicate appears below pinned chats section |

## Expected Final State

- Original chat remains pinned with pin indicator visible
- Duplicated chat is unpinned (no pin indicator)
- Both chats are accessible and separate
- Pin state is not inherited by duplicate

## Pass/Fail Criteria

**Pass:**
- Original chat remains pinned after duplication
- Duplicated chat is unpinned by default
- Pin indicator only appears on original
- Both chats are functional and separate

**Fail:**
- Duplicated chat is also pinned
- Original chat becomes unpinned
- Pin state is incorrectly inherited
- Error occurs during duplication
