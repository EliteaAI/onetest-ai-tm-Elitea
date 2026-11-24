---
id: ELITEA-3787
title: "Verify Non-Creator Participants With the Viewer Role Cannot Export, While Editor/Admin Non-Creators Can"
priority: high
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, feat:permissions, feat:roles-permissions, r-2.0.8, issue:7723]
requirements: [EliteaAI/elitea_issues#4590, EliteaAI/elitea_issues#7489, EliteaAI/elitea_issues#7723]
---
# ELITEA-3787: Verify Non-Creator Participants With the Viewer Role Cannot Export, While Editor/Admin Non-Creators Can

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that a non-creator chat participant with the Viewer project role cannot export the chat through any UI path, and that after the participant's role is changed to Editor or Admin, Export becomes available and works.

**Coverage:**
- Viewer non-creator cannot export via the "⋮" menu
- Viewer non-creator cannot export via conversation settings, toolbar or any other UI path
- Same non-creator gets Export after the role is changed to Editor, then Admin
- Creator keeps Export throughout

## Preconditions

- Team project with two user accounts:
  - User A (conversation creator, Admin role on the project)
  - User B (non-creator, **Viewer** role on the project)
- Conversation created by User A and shared with User B via "⋮" > Share > Team (selected people) > Save

## Test Data

- Conversation created by User A, with at least one message

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B (Viewer) | User B logged in successfully |
| 2 | Navigate to shared conversation | Conversation accessible to User B |
| 3 | Verify User B can view messages | Messages visible and readable |
| 4 | Open the "⋮" menu of the conversation in the list | Menu appears |
| 5 | Verify "Export" option NOT in menu | Export NOT available in the menu |
| 6 | Click "Share" | No window opens; link copied with toast "Link copied. Only people with access can open it." |
| 7 | Open conversation | Conversation opens |
| 8 | Check for Export option in conversation settings menu (if any) | No Export option in settings |
| 9 | Check toolbar or action buttons | No Export button or action |
| 10 | Check any other UI locations for Export | No Export capability anywhere; the Export chat window cannot be opened |
| 11 | Log out User B and log in as User A | User A logged in |
| 12 | Verify User A (creator) can still access Export | Export option visible in the "⋮" menu |
| 13 | Verify User A can export successfully | Export succeeds, file downloads |
| 14 | As User A, change User B's project role to Editor in Settings > Users | Role saved |
| 15 | Log in as User B, open the conversation and its "⋮" menu | Export option VISIBLE |
| 16 | Click "Export", then "Export" in the window | Export succeeds, file downloads |
| 17 | As User A, change User B's role to Admin; as User B repeat steps 15-16 | Export option visible; export succeeds |

## Expected Final State

- User B with the Viewer role cannot export through any UI path
- User B with the Editor or Admin role can export
- User A (creator) retains full export capability

## Pass/Fail Criteria

**Pass:**
- User B (Viewer) does NOT see Export in the menu, settings, toolbar or any UI path
- User B (Editor, Admin) sees Export and exports successfully
- User A (creator) can export successfully

**Fail:**
- User B (Viewer) can see Export or open the Export chat window
- User B (Editor/Admin) cannot see or use Export
- User A (creator) cannot export

## Postconditions

- Conversation unchanged
- Restore User B's role to Viewer
