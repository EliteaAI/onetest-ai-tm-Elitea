---
id: ELITEA-4477
title: "The Restore file picker filters out a file with a non-matching extension at the OS dialog level, and attempting to select an unrelated real file (correct extension, wrong content) is rejected with a clear error and no data written"
priority: high
type: security
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, security, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4477: Restore file picker rejects a wrong file type outright

**Module:** Project Backup & Restore · **Priority:** High · **Type:** Security

### Preconditions
- A plain `.txt` file (any content) saved somewhere accessible.
- A valid single-chat export file (produced via the separate chat Export feature, `.json.enc` or `.zip.enc`)
  — used here only as an example of a real file that shares the backup's encrypted-envelope format but is
  **not** a project backup.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Open "Restore from the Backup", click "Choose a backup file", browse to the folder containing the `.txt` file. | The `.txt` file is **not visible/selectable** in the picker at all — filtered out at the OS dialog level by the accepted-extensions filter (`.enc`, `.sql`, `.zip`). |
| 2 | Select and attempt to restore the chat-export file instead (matching extension, wrong content/feature). | The file is rejected with a clear error (e.g. "unrecognized backup file" / equivalent) before any data is written. No chat, agent, or other entity is created/modified in the target project. |

### Expected Final State
Only genuine project backup files are ever accepted; a wrong-extension file is filtered before selection, and a wrong-content-but-matching-extension file is safely rejected with no data written.

### Pass/Fail Criteria
**Pass:** The `.txt` file is unselectable; the chat-export file is rejected cleanly with no data change.
**Fail:** Either file is accepted as a valid project backup, or any partial data is written despite the rejection.
