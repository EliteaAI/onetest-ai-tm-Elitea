---
id: ELITEA-4988
title: "Granting and revoking team Admin changes access without a new login"
priority: high
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [feat:roles-permissions, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7507]
---

**Objective:** In a team project, Admin can still be granted and revoked, and the member's access follows each change in the same session, without logging out.

## Preconditions

- User A (Admin of team project T) and User B are available. Accounts, API calls and probes: [test-data/private-project-owner-admin](../../../../test-data/private-project-owner-admin/README.md)
- User B is logged in in a separate browser session and is not a member of T

## Test Data

| B's role in T | Admin-only permissions | Delete probe (GET / POST) | Restore probe | Delete Project Data + "Restore from the Backup" |
|---|---|---|---|---|
| Editor | None | 403 / 403 | 403 | Hidden |
| Admin | All | 200 / 400 | 400 | Shown |
| Viewer | None | 403 / 403 | 403 | Hidden |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, add User B to T as Editor | `GET admin/users/default/{T id}` shows B with `editor` |
| 2 | As User B, call `GET auth/permissions/prompt_lib/{T id}`, run both probes, and open T's Settings → General | Editor row |
| 3 | As User A, `PUT admin/users/default/{T id}` `{"id": <B id>, "roles": ["admin"]}` | B shows `admin` |
| 4 | In B's **same** session (no logout), repeat step 2 (reload the page) | Admin row |
| 5 | As User A, change B's roles to `["viewer"]` | B shows `viewer` |
| 6 | In B's same session, repeat step 2 | Viewer row |
| 7 | As User A, remove User B from T | B is no longer a member |

## Expected Final State

B's access matched each role as soon as it was changed; B is not a member of T.

## Pass/Fail Criteria

**Pass:**
- Every row of the Test Data table matches without B logging in again

**Fail:**
- Admin can't be granted in a team project
- B keeps admin-only access after the change to Viewer, or needs a new login to get or lose it
