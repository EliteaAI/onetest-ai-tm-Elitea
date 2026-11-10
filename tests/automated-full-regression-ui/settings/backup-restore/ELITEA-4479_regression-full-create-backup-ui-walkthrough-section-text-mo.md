---
id: ELITEA-4479
title: "[Regression] Full Create Backup UI walkthrough — section text, modal defaults, all 3 Chats options' exact filenames, and the 'Backup downloaded.' toast"
priority: critical
type: regression
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, regression, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4479: [Regression] Create Backup: full E2E UI walkthrough, download, and toast

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Regression

### Preconditions
- A project ("Project A") containing 1 chat with 1 attachment (upload 1 file as the user after any first
  message).

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Go to Settings → General → Back Up & Restore section. Read its description text. | Reads exactly: **"Back up this project's data to be able to restore it, if needed. Your backup will be downloaded as an encrypted file and will include agents, pipelines, toolkits, MCP servers and skills, and optionally all chats with or without their attachments. Credentials, tokens and other secrets will be excluded from this backup file and cannot be restored."** **"Create a Backup"** and **"Restore from the Backup"** buttons are present. |
| 2 | Click **"Create a Backup"**. | Modal "Create Project Backup" opens; "Do not include chats" selected by default; Cancel/Backup present; no file downloads yet. |
| 3 | Select **"Do not include chats"**, click Backup. | Button shows **"Preparing..."** and disables while in flight. Downloads `elitea-backup-<id>-<slug>-safe-<ts>.sql.enc` (no `-chats-` segment). Toast **"Backup downloaded."** appears. |
| 4 | Reopen, select **"All chats without attachments"**, click Backup. | Downloads `elitea-backup-<id>-<slug>-safe-chats-<ts>.sql.enc`. Toast **"Backup downloaded."** appears again. |
| 5 | Reopen, select **"All chats with attachments"**, click Backup. | Downloads `elitea-backup-<id>-<slug>-safe-chats-files-<ts>.zip.enc`. Toast **"Backup downloaded."** appears again. |

### Expected Final State
The full Create Backup UI path — section text, modal, all 3 filename patterns, and the download-confirmation toast — works correctly end to end.

### Pass/Fail Criteria
**Pass:** Section/modal text matches exactly; all 3 downloads succeed with the exact correct filename pattern; the "Backup downloaded." toast appears every time.
**Fail:** Any text mismatch, wrong filename/extension, missing/wrong toast, or any download failing.
