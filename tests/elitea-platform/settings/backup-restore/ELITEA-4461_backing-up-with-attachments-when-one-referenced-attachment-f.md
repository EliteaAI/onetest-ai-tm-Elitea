---
id: ELITEA-4461
title: "Backing up 'with attachments' when one referenced attachment file is already missing from storage still completes, with the exact warning toast naming the missing-file count"
priority: critical
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4461: Backup with a missing attachment file: warning toast, backup still completes

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Functional

### Preconditions
- A project ("Project A") containing one chat: send a first message, then have an **Agent/tool generate 2
  files** directly into the Artifacts bucket as part of its response.
- Direct access to the project's Artifacts bucket to delete a file (not via the chat message's own delete
  control — deleting through the message also removes the message's reference, which is a different scenario
  not covered here).

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Delete **one** of the 2 generated files directly from the Artifacts bucket. The chat message still references it (its text/attachment row is untouched). | 1 of 2 attachments is now missing from storage while still referenced by the chat. |
| 2 | Open "Create Project Backup", select **"All chats with attachments"**, click **Backup**. | Backup **completes successfully** (does not error out). A warning toast appears, reading exactly: **"Backup created. 1 attachment file(s) could not be included."** |
| 3 | Restore this backup (Preview only, any project) selecting **"Restore all chats with attachments"**. | Dry-run summary still reports both attachment-message occurrences in its attachment count (the backup legitimately knows 2 attachment references existed, even though only 1 file's content could be packed) — this is expected, not a miscount. |

### Expected Final State
A missing file at backup time never blocks the backup; it is reported via the exact warning toast and reflected consistently in downstream attachment counts.

### Pass/Fail Criteria
**Pass:** Backup completes; toast text matches exactly with the correct count.
**Fail:** Backup errors out, toast text/count wrong, or missing/misleading toast.
