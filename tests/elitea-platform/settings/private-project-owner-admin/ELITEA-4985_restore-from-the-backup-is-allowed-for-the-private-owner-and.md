---
id: ELITEA-4985
title: "Restore from the Backup is allowed for the private owner and team Admin only"
priority: high
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [feat:roles-permissions, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7507]
---

**Objective:** Restore, another admin-only feature, follows the same rule as Delete Project Data: allowed for the owner of a private project and a team Admin, denied for Editors, Viewers and non-members.

## Preconditions

- User A (owner of P-A, Admin of T) and User B are available. Accounts and API calls: [test-data/private-project-owner-admin](../../../../test-data/private-project-owner-admin/README.md)
- User B is not a member of T or P-A
- DevTools → Network is open to watch for `POST .../admin/project_restore/...` requests

## Test Data

| Caller | Project | "Restore from the Backup" | Restore probe (`POST admin/project_restore/prompt_lib/{id}`, no file) |
|---|---|---|---|
| User A (owner) | P-A | Shown | 400 "no file provided" |
| User A (Admin) | T | Shown | 400 "no file provided" |
| User B (Editor) | T | Hidden | 403 `access_denied` |
| User B (Viewer) | T | Hidden, no Back up & Restore section | 403 `access_denied` |
| User B (no access) | P-A | Hidden | 403 `access_denied` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, open Settings → General of P-A → Back up & Restore → **Restore from the Backup** | The restore modal opens; **Restore** is disabled until a file is chosen |
| 2 | Click **Cancel** | The modal closes; no `project_restore` request was sent |
| 3 | As User A, run the restore probe on P-A and on T, and check the button on T's General | Rows 1–2 of the table |
| 4 | As User A, add User B to T as Editor. As User B, open T's General and run the probe | Row 3 |
| 5 | As User A, change B's role in T to Viewer. As User B, repeat | Row 4 |
| 6 | As User B, run the probe on P-A | Row 5 |
| 7 | As User A, remove User B from T | B is no longer a member |

## Expected Final State

Only User A could reach Restore; nothing was restored.

## Pass/Fail Criteria

**Pass:**
- Every row of the Test Data table matches, and no restore request is sent from the UI

**Fail:**
- The owner or team Admin is denied, or any Editor/Viewer/non-member call passes authz (400) or sees the button
