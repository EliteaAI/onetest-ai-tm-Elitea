---
id: ELITEA-4987
title: "Only the owner holds Admin in a private project when a member is added or promoted"
priority: critical
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [feat:roles-permissions, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7507]
---

**Objective:** The owner-only Admin guard strips `admin` for anyone but the owner of a private project, both when a member is added and when their roles are changed.

## Preconditions

- User A (owner of P-A) and User B are available. Accounts and API calls: [test-data/private-project-owner-admin](../../../../test-data/private-project-owner-admin/README.md)
- User B is not a member of P-A. Note the "Teammates: N" count on P-A's Settings → General

## Test Data

| Field | Value |
|-------|-------|
| Add | `POST {{base_url}}/api/v2/admin/users/default/{P-A id}` `{"emails": ["<B email>"], "roles": ["admin", "editor"]}` |
| Promote | `PUT {{base_url}}/api/v2/admin/users/default/{P-A id}` `{"id": <B id>, "roles": ["admin"]}` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, send the Add request | B becomes a member of P-A with `editor` and without `admin` (`GET admin/users/default/{P-A id}`) |
| 2 | As User A, send the Promote request | B still has no `admin`; User A still holds `admin` |
| 3 | Reload P-A's Settings → General | "Teammates" is one higher than before; User A still sees Delete Project Data |
| 4 | As User A, remove B from P-A | B is no longer a member |

## Expected Final State

User A is the only Admin of P-A; B is not a member.

## Pass/Fail Criteria

**Pass:**
- B never holds `admin` in P-A, after the add or the promote
- User A keeps `admin`

**Fail:**
- B holds `admin` at any point, or User A loses it

## Notes

Both requests answer 200 even though `admin` was dropped (the guard strips it without saying so). Record the response text; see also ELITEA-4990 and ELITEA-4995.
