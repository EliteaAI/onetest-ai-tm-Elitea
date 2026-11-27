---
id: ELITEA-4986
title: "Private owner holds every admin-only permission; Editor and Viewer members hold none"
priority: high
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [feat:roles-permissions, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7507]
---

**Objective:** The owner's effective permissions include every admin-only permission and everything an Editor or Viewer has, and no Editor or Viewer, in a private or a team project, gets an admin-only permission.

## Preconditions

- User A (owner of P-A, Admin of T) and User B are available. User B is not a member of P-A or T. Accounts, API calls and the admin-only list: [test-data/private-project-owner-admin](../../../../test-data/private-project-owner-admin/README.md)

## Test Data

| Caller | Project | Admin-only permissions held |
|---|---|---|
| User A (owner) | P-A | All of them |
| User B (Editor) | P-A | None |
| User B (Viewer) | P-A | None |
| User B (Editor) | T | None |
| User B (Viewer) | T | None |

Permissions API: `GET {{base_url}}/api/v2/auth/permissions/prompt_lib/{project_id}`

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, call the permissions API for P-A | The list has every admin-only permission |
| 2 | As User A, add User B to P-A as Editor. As User B, call the permissions API for P-A | No admin-only permission. Every permission B has is also in User A's list from step 1 |
| 3 | As User B, open P-A's Settings → General | No Delete Project Data section and no **Restore from the Backup** button. **Create a Backup** is shown (by design, see Notes) |
| 4 | As User A, change B's role in P-A to Viewer. As User B, call the permissions API | No admin-only permission; every permission is also in User A's list |
| 5 | As User A, remove B from P-A and add B to T as Editor, then as Viewer; as User B call the permissions API for T each time | No admin-only permission in either role |
| 6 | As User A, remove User B from T | B is not a member of P-A or T |

## Expected Final State

Admin-only permissions are held only by the owner; B is not a member of P-A or T.

## Pass/Fail Criteria

**Pass:**
- Every row of the Test Data table matches
- User A's permissions in P-A include all of B's Editor and Viewer permissions there

**Fail:**
- The owner misses an admin-only permission, or one that B has as Editor/Viewer
- B holds any admin-only permission in any row

## Notes

`models.project_backup` and `models.project_backup.download` are **not** admin-only: an Editor may download a backup by design. Don't count them as a failure.
