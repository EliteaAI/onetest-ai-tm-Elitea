---
id: ELITEA-3786
title: "Verify Export Option Visibility for the Chat Creator and Non-Creator Participants by Project Role"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, feat:permissions, feat:roles-permissions, r-2.0.8, issue:7723]
requirements: [EliteaAI/elitea_issues#4590, EliteaAI/elitea_issues#7489, EliteaAI/elitea_issues#7723]
---
# ELITEA-3786: Verify Export Option Visibility for the Chat Creator and Non-Creator Participants by Project Role

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that the "Export" option in the chat "⋮" menu is available to the chat creator and to non-creator participants with the Editor or Admin project role, and is NOT available to non-creator participants with the Viewer project role.

**Coverage:**
- Creator sees Export option and can export successfully
- Non-creator participant with Viewer role does NOT see Export option
- Non-creator participant with Editor role sees Export option and can export
- Non-creator participant with Admin role sees Export option and can export

## Preconditions

- Team project with three user accounts:
  - User A (conversation creator, Admin or Editor role)
  - User V (non-creator, **Viewer** role on the project)
  - User E (non-creator, **Editor** role on the project); for the Admin check, switch User E's role to Admin
- Conversation created by User A and shared with User V and User E via "⋮" > Share > Team (selected people) > Save
- Users can be logged in sequentially

## Test Data

- Conversation "Test Conversation" created by User A, with at least one message

## Steps

### Steps (as User A - Creator):

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User A | User A logged in successfully |
| 2 | Navigate to Chats section | Chat list visible |
| 3 | Locate "Test Conversation" created by User A | Conversation visible in list |
| 4 | Open the "⋮" menu of "Test Conversation" | Menu appears |
| 5 | Verify "Export" option present in menu | **Export option VISIBLE** |
| 6 | Click "Export" | Export chat window opens |
| 7 | Click "Export" in the window | Export succeeds, file downloads |

### Steps (as User V - Non-Creator, Viewer role):

| # | Action | Expected Result |
|---|--------|----------------|
| 8 | Log out and log in as User V | User V logged in successfully |
| 9 | Navigate to shared conversation "Test Conversation" | Conversation visible (User V is a participant) |
| 10 | Verify User V can view conversation messages | Messages readable |
| 11 | Open the "⋮" menu of "Test Conversation" | Menu appears |
| 12 | Verify "Export" option **NOT** present in menu | **Export option NOT VISIBLE** |
| 13 | Verify available options | "Share" is present and only copies the link (toast "Link copied. Only people with access can open it."); no Export, no Delete |
| 14 | Check conversation settings/toolbar (if any) | No Export option in settings or toolbar |
| 15 | Verify User V cannot open the Export chat window through any means | No export capability available to User V |

### Steps (as User E - Non-Creator, Editor/Admin role):

| # | Action | Expected Result |
|---|--------|----------------|
| 16 | Log out and log in as User E (Editor role) | User E logged in successfully |
| 17 | Open "Test Conversation" and its "⋮" menu | **Export option VISIBLE** |
| 18 | Click "Export", then "Export" in the window | Export succeeds, file downloads |
| 19 | As User A, change User E's project role to Admin; log in as User E again and repeat steps 17-18 | Export option visible; export succeeds |

## Expected Final State

- User A (creator) sees Export and can export successfully
- User V (non-creator, Viewer) does NOT see Export anywhere
- User E (non-creator, Editor or Admin) sees Export and can export successfully

## Pass/Fail Criteria

**Pass:**
- User A sees "Export" and exports successfully
- User V (Viewer) does NOT see "Export" and cannot open the Export chat window through any UI path
- User E sees "Export" and exports successfully with both Editor and Admin roles

**Fail:**
- User A cannot see or use Export
- User V (Viewer) can see Export or open the Export chat window
- User E (Editor/Admin) cannot see or use Export

## Postconditions

- Conversation unchanged
- Restore User E's original project role
