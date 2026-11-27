---
id: ELITEA-5000
title: "Admin of an own private project gives no access to other projects or the platform"
priority: critical
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:roles-permissions, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7507]
---

# ELITEA-5000: Admin of an own private project gives no access to other projects or the platform

**Module:** settings-users-and-roles · **Priority:** critical · **Type:** functional

**Objective:** User B's Admin role in their own private project is scoped to that project: it grants nothing in a team project where B is a Viewer, in another user's private project, or on the platform.

---

## Preconditions

- User A (owner of P-A, Admin of T) and User B (owner of P-B, not a platform admin) are available. Accounts and API calls: [test-data/private-project-owner-admin](../../../../test-data/private-project-owner-admin/README.md)
- User A adds User B to T as **Viewer**. B is not a member of P-A

---

## Test Data

| Project (as User B) | Roles | Delete Project Data section | Delete probe (GET / POST) |
|---|---|---|---|
| P-B (own private) | `admin`, `editor`, `viewer` | Shown | 200 / 400 |
| T (Viewer) | `viewer` | Hidden | 403 / 403 |
| P-A (no access) | — | Hidden | 403 / 403 |
| Platform admin endpoint `GET {{base_url}}/api/v2/admin/projects/administration` | — | — | 403 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User B, call `GET admin/users/default/{P-B id}` | B holds `admin`, `editor`, `viewer` in P-B |
| 2 | As User B, open Settings → General of P-B and run the delete probe | Section shown; probe 200 / 400 |
| 3 | As User B, open Settings → General of T and run the delete probe | General opens, section hidden; probe 403 / 403 |
| 4 | As User B, open `{{base_url}}/app/{P-A id}/settings/project-general` and run the delete probe on P-A | No Delete Project Data section; probe 403 / 403 |
| 5 | As User B, call the platform admin endpoint | 403 |
| 6 | As User A, remove User B from T | B is no longer a member of T |

---

## Expected Final State

B's admin rights exist only in P-B; B is not a member of T or P-A.

---

## Pass/Fail Criteria

**Pass:**
- Every row of the Test Data table matches

**Fail:**
- B gets 200/400 on the probe in T or P-A, sees the section there, or gets 200 from the platform endpoint

---

## Notes

- **Source functional tests:** ELITEA-4986 (`tests/elitea-platform/settings/private-project-owner-admin/`)
- **Regression rationale:** The cross-project / privilege-escalation risk of #7507: granting Admin to every private owner must not widen anyone's reach.
- **Selectors (`data-testid`):** `project-general-section`, `project-data-delete-section`
- User B must not be a platform admin, or step 5 can't fail. Check `GET auth/user` in B's context is B before the run.
- P-A as User B may redirect or show an access error instead of General; the assertion is only that no `project-data-delete-section` is rendered and the probe is 403.
- All of B's calls go through B's own session (second browser context); only the membership setup and cleanup run as User A.
- Remove B from T in a `finally` block. Dismiss B's "What's New" modal before screenshots.
