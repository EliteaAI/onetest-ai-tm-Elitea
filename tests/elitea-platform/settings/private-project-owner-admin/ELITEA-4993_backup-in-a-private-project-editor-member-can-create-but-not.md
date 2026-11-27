---
id: ELITEA-4993
title: "Backup in a private project: Editor member can create but not restore, Viewer has no access"
priority: medium
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [feat:roles-permissions, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7507]
---

**Objective:** With the owner now Admin, the backup roles in a private project stay as designed: the owner can back up and restore, an Editor member can back up but not restore, and a Viewer has no access.

## Preconditions

- User A (owner of P-A) and User B are available. Accounts, API calls and probes: [test-data/private-project-owner-admin](../../../../test-data/private-project-owner-admin/README.md)
- User B is not a member of P-A
- DevTools → Network is open to watch for backup download requests (`.../project_backup/prompt_lib/...`)

## Test Data

| Caller in P-A | Back up & Restore section | Backup summary `GET admin/project_backup_summary/prompt_lib/{P-A id}` | Restore probe |
|---|---|---|---|
| User A (owner) | "Create a Backup" and "Restore from the Backup" | 200 | 400 |
| User B (Editor) | "Create a Backup" only | 200 | 403 |
| User B (Viewer) | Not shown | 403 | 403 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, call the backup summary API and note `chats_count` | 200 |
| 2 | Open P-A's Settings → General → **Create a Backup** | The "Create Project Backup" dialog opens; its chats count equals `chats_count`, and the Backup button is enabled |
| 3 | Click **Cancel** | The dialog closes; no backup download request was sent |
| 4 | As User A, add User B to P-A as Editor. As User B, open P-A's General, call the summary API and run the restore probe | Editor row |
| 5 | As User A, change B's role to Viewer. As User B, repeat | Viewer row |
| 6 | As User A, remove B from P-A | B is not a member |

## Expected Final State

No backup was made or restored; B is not a member of P-A.

## Pass/Fail Criteria

**Pass:**
- Every row of the Test Data table matches
- The dialog's chats count equals the API

**Fail:**
- An Editor can restore or sees "Restore from the Backup"
- A Viewer sees the section or gets 200 on the summary
- The owner can't back up or restore

## Notes

Downloading a backup is an Editor action by design (admin `module.py`: viewers are excluded because a full export is bulk data egress; Restore stays admin-only). A team project whose stored Editor role predates this default may lack `models.project_backup.download` (seen on DEV 2026-11-27); this case uses a private project to avoid that.
