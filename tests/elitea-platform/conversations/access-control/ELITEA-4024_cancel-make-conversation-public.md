---
id: ELITEA-4024
title: "Cancel Making Conversation Public"
priority: high
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, make-public, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-4024: Cancel Making Conversation Public

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that canceling the "Make public" confirmation dialog does not change the conversation's access state.

## Preconditions

- Logged in to {{base_url}} as conversation creator/author
- A private conversation exists in a team project
- Conversation is currently NOT public (grey sharing icon)

## Test Data

| Field | Value |
|-------|-------|
| User Role | Conversation Author |
| Initial State | Private conversation |
| Project Type | Team project |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Chats in sidebar | Conversation list is displayed |
| 2 | Right-click on the private conversation | Action dropdown menu opens |
| 3 | Click "Make public" option | Confirmation dialog appears |
| 4 | Verify dialog displays correctly | Title: "Public conversation?", Message: "Are you sure to make your conversation public?", Buttons: Cancel, Make public |
| 5 | Click "Cancel" button | Dialog closes |
| 6 | Verify conversation state in sidebar | Sharing icon remains grey (private) |
| 7 | Right-click conversation again | "Make public" option is still visible |
| 8 | Login as another project member | Member cannot access the conversation (still private) |

## Expected Final State

- Conversation remains private
- Sharing icon stays grey
- No audit log entry for access change
- Other project members still cannot access

## Teardown

- None required
