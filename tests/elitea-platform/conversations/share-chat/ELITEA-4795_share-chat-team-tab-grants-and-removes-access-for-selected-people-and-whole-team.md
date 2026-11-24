---
id: ELITEA-4795
title: "Share Chat Team tab grants and removes access for selected people and Whole team"
priority: critical
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4795: Share Chat Team tab grants and removes access for selected people and Whole team

**Module:** conversations · **Priority:** critical · **Type:** functional

**Objective:** Verify that the owner can grant access to selected people and to the whole team, remove it, and that access really follows what is saved.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Team project with at least 3 members: User A (owner), User B, User C. User B and User C have separate sessions.
- Chat C1 owned by User A, only the owner has access.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, open Share > Team | Search "Add people from the team project". "People with access – 1". Only User A, with the badge "Owner" and no ×. Save is disabled |
| 2 | Focus the search, pick User B and User C, click Add | User B and User C are listed after the owner in the order added. Count = 3. Save is enabled |
| 3 | Click Save | Toast "Access updated". The window stays open. Save is disabled again |
| 4 | As User B and as User C, open the URL of C1 | Both can open and read the chat |
| 5 | As User A, hover the row of User C, click ×, then Save | User C is removed. Count = 2. Toast "Access updated" |
| 6 | As User C, reload C1 and open it by direct URL | User C cannot open the chat; it is not in User C's chat list |
| 7 | As User A, pick "Whole team: <n> teammates", click Add, then Save | The list of people is replaced by Whole team. Count = all project members (owner included). The Users card shows "Whole Team (N)" without reload |
| 8 | As User C, open C1 | User C can open the chat |
| 9 | As User A, click "Remove access for all", then Save | Only the owner is left. Count = 1. User B and User C cannot open the chat by direct URL |

---

## Expected Final State

Access to the chat matches the saved list; the owner always keeps access.
