---
id: ELITEA-4987
title: "Admin guard on an existing private-project member with mixed and admin-only role lists"
priority: high
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [feat:roles-permissions, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7507]
---

**Objective:** A role change that includes `admin` for an existing non-owner member of a private project never gives them Admin or any admin-only feature.

## Preconditions

- User A (owner of P-A) and User B are available. Accounts, API calls and probes: [test-data/private-project-owner-admin](../../../../test-data/private-project-owner-admin/README.md)
- User A adds User B to P-A as **Viewer**

## Test Data

| Field | Value |
|-------|-------|
| Mixed PUT | `PUT {{base_url}}/api/v2/admin/users/default/{P-A id}` `{"id": <B id>, "roles": ["admin", "editor"]}` |
| Admin-only POST on the member | `POST {{base_url}}/api/v2/admin/users/default/{P-A id}` `{"emails": ["<B email>"], "roles": ["admin"]}` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, send the Mixed PUT | 200. B now has `editor` and no `admin` (`GET admin/users/default/{P-A id}`) |
| 2 | As User A, send the Admin-only POST | 400 "already exists"; B still has no `admin`; User A still holds `admin` |
| 3 | As User B, call `GET auth/permissions/prompt_lib/{P-A id}` | No admin-only permission |
| 4 | As User B, run the Delete Project Data probe and the Restore probe on P-A | Delete GET/POST 403/403; Restore 403 |
| 5 | As User B, open P-A's Settings → General | No Delete Project Data section and no **Restore from the Backup** button |
| 6 | As User A, remove B from P-A | B is no longer a member |

## Expected Final State

User A is the only Admin of P-A; B is not a member.

## Pass/Fail Criteria

**Pass:**
- B ends with `editor` (or editor + viewer), never `admin`
- All of B's probes are denied, and the admin-only UI is hidden for B

**Fail:**
- B holds `admin` or any admin-only permission, or any of B's probes passes authz

## Notes

Step 1 answers 200 "roles updated" while only `editor` is applied, so the caller isn't told that `admin` was dropped. Record the response; this is not a failure of this case.
