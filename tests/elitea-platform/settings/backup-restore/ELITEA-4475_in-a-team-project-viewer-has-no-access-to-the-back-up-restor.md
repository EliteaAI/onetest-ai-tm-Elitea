---
id: ELITEA-4475
title: "In a team project, Viewer has no access to the Back Up & Restore section at all, Editor can create backups but not restore, and Admin can do both; in a private project, its owner always has both regardless of their underlying role"
priority: high
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, permissions, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4475: Role-based access to Backup/Restore, including the private-project-owner exception

**Module:** Project Backup & Restore · **Priority:** High · **Type:** Functional

### Preconditions
- A team project ("Project A") with a second test account ("User B") whose project role can be switched
  between Viewer, Editor, and Admin.
- User B's own private project ("Project B-Private"), where User B is the owner.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Set User B's role in Project A to **Viewer**. Log in as User B, go to Settings → General. | The **Back Up & Restore section is not shown at all** (not just disabled — absent). |
| 2 | Set User B's role to **Editor**. Repeat. | Section is visible. **"Create a Backup" is present and works** (produces a successful backup). **"Restore from the Backup" is not available.** |
| 3 | Set User B's role to **Admin**. Repeat. | Both **"Create a Backup"** and **"Restore from the Backup"** are available and work. |
| 4 | As User B, open Project B-Private's Settings → General (User B's own private project, independent of any team-project role). | Both **"Create a Backup"** and **"Restore from the Backup"** are available to User B here — because User B is the private project's owner, not because of any Admin/Editor/Viewer role (which doesn't apply to a private project the same way). |

### Expected Final State
Backup/Restore visibility correctly follows the team-project role matrix (Viewer: none, Editor: backup only, Admin: both), with private-project ownership as an independent, always-both exception.

### Pass/Fail Criteria
**Pass:** All 4 steps match exactly.
**Fail:** Any role seeing the wrong set of options, or a private project owner missing either option.
