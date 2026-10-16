---
id: ELITEA-2636
title: "Duplicate Naming Convention - Unique Names with 'Copy of' or Numbered Suffix"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [chat, duplicate, naming, P1]
requirements: [3837]
---
# ELITEA-2636: Duplicate Naming Convention - Unique Names with 'Copy of' or Numbered Suffix

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that duplicated chats receive unique names with proper naming convention (e.g., "Copy of..." or "chat_name (1)") to distinguish them from the original.

## Preconditions

- User is logged in to {{base_url}}
- Original chat exists with a specific name
- User has permission to duplicate chats

## Test Data

- URL: {{base_url}}
- Original chat name: "Project Planning Chat"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Note the original chat name | Original: "Project Planning Chat" |
| 2 | Duplicate the chat (first duplication) | First duplicate created |
| 3 | Verify duplicated chat name | Name shows convention: "Copy of Project Planning Chat" OR "Project Planning Chat (1)" |
| 4 | Verify name is distinguishable from original | Suffix/prefix added |
| 5 | Duplicate the original chat again (second duplication) | Second duplicate created |
| 6 | Verify second duplicate has unique name | Name: "Copy of Project Planning Chat (1)" OR "Project Planning Chat (2)" |
| 7 | Duplicate the first duplicate | Third chat created |
| 8 | Verify third duplicate has unique name | Naming increments appropriately |
| 9 | Verify all chats have unique names in list | No name collisions |
| 10 | Test with special characters in original name | Special characters handled correctly |

## Expected Final State

- Each duplicated chat has unique name
- Naming convention applied consistently
- Names distinguishable from original
- No name collisions

## Pass/Fail Criteria

**Pass:**
- Duplicate names follow convention ("Copy of..." or numbered)
- Each duplicate has unique name
- Names distinguishable in chat list
- Multiple duplicates increment correctly
- Special characters handled safely

**Fail:**
- Duplicate has identical name to original
- Name collisions occur
- No suffix/prefix added
- Naming convention inconsistent
- Special characters cause errors
