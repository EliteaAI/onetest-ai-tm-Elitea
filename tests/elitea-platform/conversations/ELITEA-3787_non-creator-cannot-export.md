---
id: ELITEA-3787
title: "Verify Non-Creator Users Cannot Export Conversation"
priority: high
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, feat:permissions, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590, EliteaAI/elitea_issues#7489]
---
# ELITEA-3787: Verify Non-Creator Users Cannot Export Conversation

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that users who did not create a conversation cannot export it, even if they have viewing or editing permissions.

**Coverage:**
- Non-creator cannot export via context menu
- Non-creator cannot export via conversation settings
- Non-creator cannot export via any other UI path
- Permissions verified for users with different access levels

## Preconditions

- Two user accounts:
  - User A (conversation creator)
  - User B (collaborator with view/edit access but not creator)
- Conversation created by User A and shared with User B via "⋮" > Share > Team (selected people) > Save
- User B has permissions to view and possibly edit messages, but is not the creator

## Test Data

- Conversation created by User A
- User B has collaborative access (viewing, possibly editing)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B | User B logged in successfully |
| 2 | Navigate to shared conversation | Conversation accessible to User B |
| 3 | Verify User B can view messages | Messages visible and readable |
| 4 | If User B has edit permissions, verify can send messages | User B can participate in conversation (if edit access granted) |
| 5 | Right-click conversation in list | Context menu appears |
| 6 | Verify "Export" option NOT in menu | Export NOT available in context menu |
| 7 | Click "Share" | No window opens; link copied with toast "Link copied. Only people with access can open it." |
| 8 | Open conversation | Conversation opens |
| 9 | Check for Export option in conversation settings menu (if any) | No Export option in settings |
| 10 | Check toolbar or action buttons | No Export button or action |
| 11 | Check any other UI locations for Export | No Export capability anywhere |
| 12 | Verify User B cannot trigger export through any means | Export completely restricted to User B |
| 13 | Log out User B and log in as User A | User A logged in |
| 14 | Verify User A (creator) can still access Export | User A right-clicks → Export option visible |
| 15 | Verify User A can export successfully | User A exports successfully, confirming creator privilege |

## Expected Final State

- User B (non-creator) cannot export through any UI path
- User A (creator) retains full export capability
- Permission enforcement correct

## Pass/Fail Criteria

**Pass:**
- User B (non-creator) does NOT see Export in context menu
- User B cannot find Export in conversation settings
- User B cannot export through any UI path (toolbar, settings, menus)
- User A (creator) can still export successfully
- Permissions correctly enforced

**Fail:**
- User B can access Export through any means
- Export available to non-creator in any UI location
- User A (creator) cannot export
- Permission enforcement fails

## Postconditions

- Conversation unchanged
- User A retains creator export privileges
- User B retains collaborative access without export
