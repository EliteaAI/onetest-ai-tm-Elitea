---
id: ELITEA-4595
title: "[Regression] Viewer has no Backup/Restore access, Editor can only create backups, Admin can do both, in a team project"
priority: high
type: regression
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, permissions, regression, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4595: [Regression] Role-based access to Backup/Restore

**Module:** Project Backup & Restore · **Priority:** High · **Type:** Regression

### Preconditions
- A team project with a second test account ("User B") whose role can be switched.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Set User B's role to Viewer. | Back Up & Restore section not shown at all. |
| 2 | Set to Editor. | Section visible; Create Backup works; Restore not available. |
| 3 | Set to Admin. | Both options available and work. |

### Expected Final State
Role matrix holds exactly.

### Pass/Fail Criteria
**Pass:** All 3 steps match exactly.
**Fail:** Any role seeing the wrong set of options.

---
