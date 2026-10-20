---
id: ELITEA-3786
title: "Verify Only Conversation Creator Can See/Use Export Option"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, feat:permissions, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3786: Verify Only Conversation Creator Can See/Use Export Option

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that the "Export" option in the context menu is only visible and accessible to the user who created the conversation.

**Coverage:**
- Creator sees Export option in context menu
- Creator can export conversation successfully
- Non-creator does NOT see Export option
- Non-creator cannot export through any means

## Preconditions

- Two user accounts available:
  - User A (conversation creator)
  - User B (non-creator, has access to view conversation)
- Conversation exists created by User A, shared with User B
- Both users can be logged in (test sequentially or in parallel)

## Test Data

- Conversation "Test Conversation" created by User A
- User B has viewing/collaborative access but is not the creator

## Steps

### Steps (as User A - Creator):

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User A | User A logged in successfully |
| 2 | Navigate to Chats section | Chat list visible |
| 3 | Locate "Test Conversation" created by User A | Conversation visible in list |
| 4 | Right-click "Test Conversation" | Context menu appears |
| 5 | Verify "Export" option present in menu | **Export option VISIBLE** |
| 6 | Click "Export" | Dialog opens successfully |
| 7 | Click "Export" in dialog | Export succeeds, file downloads |

### Steps (as User B - Non-Creator):

| # | Action | Expected Result |
|---|--------|----------------|
| 8 | Log out User A and log in as User B | User B logged in successfully |
| 9 | Navigate to shared conversation "Test Conversation" | Conversation visible (User B has read access) |
| 10 | Verify User B can view conversation messages | Messages readable |
| 11 | Right-click "Test Conversation" | Context menu appears |
| 12 | Verify "Export" option **NOT** present in menu | **Export option NOT VISIBLE** |
| 13 | Verify available options | Options may include: View/Open, other non-destructive actions, but NOT Export or Delete |
| 14 | Check conversation settings/toolbar (if any) | Verify no Export option in settings or toolbar |
| 15 | Verify User B cannot export through any means | No export capability available to User B |

## Expected Final State

- User A (creator) sees Export and can export successfully
- User B (non-creator) does NOT see Export option anywhere
- Permissions correctly enforced

## Pass/Fail Criteria

**Pass:**
- User A (creator) sees "Export" option in context menu
- User A can export conversation successfully
- User B (non-creator) does NOT see "Export" option in context menu
- User B cannot access export through any UI path

**Fail:**
- User A cannot see or use Export
- User B (non-creator) can see or access Export
- Export available to non-creator through any means
- Permissions not enforced

## Postconditions

- Conversation unchanged
- Permissions remain correct
- User A retains creator privileges
