---
id: ELITEA-4986
title: "Admin of an own private project gives no access to other projects or the platform"
priority: critical
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [feat:roles-permissions, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7507]
---

**Objective:** User B's Admin role in their own private project is scoped to that project: it grants nothing in a team project where B is a Viewer, in another user's private project, or on the platform.

## Preconditions

- User A (owner of P-A, Admin of T) and User B (owner of P-B, not a platform admin) are available. Accounts and API calls: [test-data/private-project-owner-admin](../../../../test-data/private-project-owner-admin/README.md)
- User A adds User B to T as **Viewer**. B is not a member of P-A

## Test Data

| Project (as User B) | Roles | Delete Project Data section | Delete probe (GET / POST) |
|---|---|---|---|
| P-B (own private) | `admin`, `editor`, `viewer` | Shown | 200 / 400 |
| T (Viewer) | `viewer` | Hidden | 403 / 403 |
| P-A (no access) | — | Hidden | 403 / 403 |
| Platform admin endpoint `GET {{base_url}}/api/v2/admin/projects/administration` | — | — | 403 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User B, call `GET admin/users/default/{P-B id}` | B holds `admin`, `editor`, `viewer` in P-B |
| 2 | As User B, open Settings → General of P-B and run the delete probe | Section shown; probe 200 / 400 |
| 3 | As User B, open Settings → General of T and run the delete probe | General opens, section hidden; probe 403 / 403 |
| 4 | As User B, open `{{base_url}}/app/{P-A id}/settings/project-general` and run the delete probe on P-A | No Delete Project Data section; probe 403 / 403 |
| 5 | As User B, call the platform admin endpoint | 403 |
| 6 | As User A, remove User B from T | B is no longer a member of T |

## Expected Final State

B's admin rights exist only in P-B; B is not a member of T or P-A.

## Pass/Fail Criteria

**Pass:**
- Every row of the Test Data table matches

**Fail:**
- B gets 200/400 on the probe in T or P-A, sees the section there, or gets 200 from the platform endpoint
