---
id: ELITEA-2633
title: "Duplicate Private Chat Remains Private Unless Explicitly Shared"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
automation_test_id: []
tags: [chat, duplicate, private, visibility, P1]
requirements: [3837]
---
# ELITEA-2633: Duplicate Private Chat Remains Private Unless Explicitly Shared

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that duplicating a private (non-public) chat creates a duplicate that remains private and does not become public unless the user explicitly shares it.

## Preconditions

- User is logged in to {{base_url}}
- Team project context
- Private non-public chat exists (no green indicator)
- User has permission to manage chat visibility

## Test Data

- URL: {{base_url}}
- Team project
- Original private chat (no green indicator)
- Participant users only (not visible to non-participants)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Locate private chat in chat list | Private chat visible (no green indicator) |
| 2 | Verify original chat is NOT public | No green indicator, restricted to participants |
| 3 | Duplicate the private chat | Duplicate created successfully |
| 4 | Locate duplicated chat in chat list | Duplicated chat appears |
| 5 | Verify duplicated chat does NOT have green indicator | No green marker on duplicate |
| 6 | Log in as non-participant team member | Different user logs in |
| 7 | Verify duplicated chat NOT visible to non-participant | Chat not in list for non-participant |
| 8 | Log back in as original user | Original user session |
| 9 | Explicitly share/make duplicate public (if feature available) | Duplicate becomes public |
| 10 | Verify green indicator NOW appears on duplicate | Green indicator appears after explicit sharing |

## Expected Final State

- Duplicated chat starts as private (no green indicator)
- Non-participants cannot see duplicate
- Privacy status inherited from original
- Public status requires explicit action

## Pass/Fail Criteria

**Pass:**
- Duplicate is private by default (no green indicator)
- Non-participants cannot see duplicate
- Privacy inherited from original
- Explicit sharing required to make public
- No automatic public status change

**Fail:**
- Duplicate automatically becomes public
- Green indicator appears without explicit action
- Non-participants can see private duplicate
- Privacy not inherited
- Visibility leakage occurs
