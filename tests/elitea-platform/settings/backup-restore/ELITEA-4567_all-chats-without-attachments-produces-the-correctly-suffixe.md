---
id: ELITEA-4567
title: "'All chats without attachments' produces the correctly-suffixed filename, shows the accurate chat/attachment/size summary line, and shows the privacy note"
priority: critical
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4567: Backup output: "All chats without attachments" filename, summary line, and privacy note

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Functional

### Preconditions
- A project ("Project A") containing exactly 2 chats: Chat 1 — send the first message **"No files needed
  here"** (no attachment); Chat 2 — send a first message, then upload one file as the user (any file, e.g. a
  small text file).

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Open "Create Project Backup", select **"All chats without attachments"**. | Description below the radio group updates. A summary line appears reading exactly in the form **"\<N\> chats · \<M\> attachments · ~\<size\>"** where N = 2 and M = 1 (matching the real chat/attachment counts of Project A). |
| 2 | Observe below the summary line. | The privacy note is shown, reading exactly: **"Chats contain conversation history of all project members. Store the backup file securely."** |
| 3 | Click **Backup**. | File downloads with filename matching exactly: **`elitea-backup-<project id>-<project slug>-safe-chats-<YYYY-MM-DD>-<HH-mm-ss>.sql.enc`** (note the `-chats-` segment; extension stays `.sql.enc`, NOT a ZIP). |

### Expected Final State
Filename, summary line, and privacy note are all exact for the "without attachments" option.

### Pass/Fail Criteria
**Pass:** All 3 steps match exactly, with correct chat/attachment counts.
**Fail:** Any wording/filename mismatch, or incorrect counts in the summary line.
