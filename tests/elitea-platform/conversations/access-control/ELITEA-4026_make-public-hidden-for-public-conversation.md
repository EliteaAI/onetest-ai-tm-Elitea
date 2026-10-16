---
id: ELITEA-4026
title: "Make Public Action Hidden for Already Public Conversation"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, make-public, ui, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-4026: Make Public Action Hidden for Already Public Conversation

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "Make public" action is not displayed in the dropdown menu when a conversation is already public.

## Preconditions

- Logged in to {{base_url}} as conversation creator/author
- A PUBLIC conversation exists (sharing icon is green)

## Test Data

| Field | Value |
|-------|-------|
| User Role | Conversation Author |
| Conversation State | Public (green icon) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Chats in sidebar | Conversation list is displayed |
| 2 | Identify public conversation (green sharing icon) | Public conversation found |
| 3 | Right-click on the public conversation | Action dropdown menu opens |
| 4 | Review all available actions in dropdown | Actions displayed: Rename, Move to, Playback, Duplicate, Restrict access, Share, Share externally, Pin on top, Delete |
| 5 | Verify "Make public" is NOT present | "Make public" action is HIDDEN |
| 6 | Verify "Restrict access" IS present | "Restrict access" action is visible |

## Expected Final State

- Dropdown correctly reflects conversation's public state
- "Make public" not shown for already public conversation
- "Restrict access" available for reverting

## Teardown

- None required
