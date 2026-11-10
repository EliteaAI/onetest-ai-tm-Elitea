---
id: ELITEA-4482
title: "[Regression] Backing up 'with attachments' when a referenced file is already missing from storage still completes successfully, with the exact 'Backup created. N attachment file(s) could not be included.' toast"
priority: critical
type: regression
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, regression, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4482: [Regression] Backup with a missing attachment file still completes, with the exact warning toast

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Regression

### Preconditions
- A project ("Project A") containing 1 chat: send a first message, have an Agent/tool generate 1 file
  directly into the Artifacts bucket as part of its response.
- Direct access to delete that file from the Artifacts bucket (not via the chat message's own delete control).

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Delete the generated file directly from the Artifacts bucket (chat message still references it). | 1 attachment is missing from storage but still referenced. |
| 2 | Open "Create Project Backup", select **"All chats with attachments"**, click Backup. | Backup **completes successfully** (does not error). Warning toast appears, reading exactly: **"Backup created. 1 attachment file(s) could not be included."** |

### Expected Final State
A missing attachment at backup time never blocks the backup and is always reported via the exact warning toast.

### Pass/Fail Criteria
**Pass:** Backup completes; toast text matches exactly with the correct count.
**Fail:** Backup errors out, or the toast is missing/wrong.
