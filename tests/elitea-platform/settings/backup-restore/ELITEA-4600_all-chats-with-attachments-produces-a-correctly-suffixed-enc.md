---
id: ELITEA-4600
title: "'All chats with attachments' produces a correctly-suffixed encrypted ZIP (not a .sql.enc), covering both a user-uploaded file and an agent/tool-generated file"
priority: critical
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4600: Backup output: "All chats with attachments" produces a ZIP, covering both uploaded and agent-generated files

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Functional

### Preconditions
- A project ("Project A") containing exactly 2 chats: Chat 1 — send a first message, then **upload one file
  as the user** (any file). Chat 2 — send a first message that causes an **Agent/tool to generate a file**
  directly into the Artifacts bucket as part of its response (e.g. ask an agent with file-generation ability
  to create a short text file).

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Open "Create Project Backup", select **"All chats with attachments"**. | Summary line reads **"2 chats · 2 attachments · ~\<size\>"**. Privacy note shown (same text as TC-M04 step 2). |
| 2 | Click **Backup**. | File downloads with filename matching exactly: **`elitea-backup-<project id>-<project slug>-safe-chats-files-<YYYY-MM-DD>-<HH-mm-ss>.zip.enc`** — note the `-chats-files-` segment and the **`.zip.enc`** extension (not `.sql.enc`, confirming this option produces an archive, not a plain SQL dump). |
| 3 | Upload this same file to "Restore from the Backup" on Project A itself (or any other project), with Preview only checked. Select **"Restore all chats with attachments"**, click Preview. | Dry-run reports **"Backup contains 2 chats · 2 attachments"**; nothing written yet (Preview only). |

### Expected Final State
The "with attachments" option correctly switches the output to an encrypted ZIP, correctly covering both the user-upload and the agent-generation attachment paths.

### Pass/Fail Criteria
**Pass:** Filename ends `.zip.enc` with the `-chats-files-` segment; counts correct; both attachment sources counted.
**Fail:** Wrong extension/segment, or either attachment source (uploaded or generated) not reflected in the count.
