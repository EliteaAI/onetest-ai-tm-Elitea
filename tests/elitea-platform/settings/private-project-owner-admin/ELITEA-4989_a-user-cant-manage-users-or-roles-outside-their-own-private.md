---
id: ELITEA-4989
title: "A user can't manage users or roles outside their own private project or promote themselves"
priority: high
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [feat:roles-permissions, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7507]
---

**Objective:** Being Admin of their own private project doesn't let a user manage users or roles in other projects or raise their own role (privilege escalation).

## Preconditions

- User A (owner of P-A, Admin of T) and User B (owner of P-B) are available. Accounts, API calls and probes: [test-data/private-project-owner-admin](../../../../test-data/private-project-owner-admin/README.md)
- User A adds User B to T as **Editor**. B is not a member of P-A
- As User B, note the member list of P-B (`GET admin/users/default/{P-B id}`)

## Test Data

| Call as User B | P-B (own) | T (Editor) | P-A (no access) |
|---|---|---|---|
| Invite probe `POST admin/users/default/{id}` `{"emails": ["qa-not-an-email"], "roles": ["viewer"]}` | 400 validation error, nobody added | 403 | 403 |
| Self-promotion `PUT admin/users/default/{id}` `{"id": <B id>, "roles": ["admin"]}` | — | 403 | 403 |
| Create a role `POST admin/roles/default/{id}` `{"name": "qa_probe_role"}` | — | 403 | — |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User B, run the invite probe on P-B, T and P-A | As in the table; P-B's member list is unchanged |
| 2 | As User B, send the self-promotion PUT to T and to P-A | 403 on both |
| 3 | As User B, try to create a role in T | 403 |
| 4 | As User A, call `GET admin/users/default/{T id}` and `{P-A id}` | B is still `editor` in T and not a member of P-A |
| 5 | As User B, open T's Settings → Users | The member list is shown, with no **Invite**, **Edit** or **Delete** controls |
| 6 | As User A, remove User B from T | B is no longer a member |

## Expected Final State

B's roles are unchanged, nobody was invited, and no role was created.

## Pass/Fail Criteria

**Pass:**
- Every call in the Test Data table matches
- B's roles in T and P-A are unchanged; B's Users page in T is read-only

**Fail:**
- Any call in T or P-A passes authz, B's roles change, or Invite/Edit/Delete is shown to B in T
