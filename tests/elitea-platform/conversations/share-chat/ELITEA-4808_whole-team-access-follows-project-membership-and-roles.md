---
id: ELITEA-4808
title: "Whole team access follows project membership and roles"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4808: Whole team access follows project membership and roles

**Module:** conversations · **Priority:** high · **Type:** functional

**Objective:** Verify that Whole team access follows project membership and that project roles of users who are not the owner do not let them manage access.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Team project where User A is admin and owns chat C1 shared with Whole team ("Whole Team (N)").
- User V has the role Viewer, User E has the role Editor; User X is not in the project.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User V and as User E, open C1 and click Share in the chat menu and on the Users card | Both can open C1 within their role. Share only copies the link with a toast; no window opens |
| 2 | As User A, use "Invite to project" in Share > Team to invite User X; User X accepts | User X is a project member; C1 shows "Whole Team (N+1)"; User X can open C1 |
| 3 | As User A, remove User E from the project in Settings > Users | The count goes down; User E cannot open C1 |
| 4 | As User A, switch C1 to selected people (User V only) and Save | User X loses access; User V keeps it; counts are correct |

---

## Expected Final State

Whole team means current project members; only the owner manages access.
