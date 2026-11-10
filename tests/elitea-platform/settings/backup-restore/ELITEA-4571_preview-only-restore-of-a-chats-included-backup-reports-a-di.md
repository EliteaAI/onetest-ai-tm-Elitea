---
id: ELITEA-4571
title: "Preview-only restore of a chats-included backup reports a distinct chat-restoration count line without writing any data"
priority: critical
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4571: Restore: Preview (dry run) reports chat-specific counts and writes nothing

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Functional

### Preconditions
- A project ("Project A") containing exactly 1 chat (any first message, no attachment). Back it up with
  "All chats without attachments" to produce the test file.
- A second project ("Project B") with zero chats, to restore into.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Note Project B's current chat count (0) and non-chat-entity state. | Baseline recorded. |
| 2 | In Project B, open "Restore from the Backup", upload the file from Project A. Leave **Preview only** checked (default). Select **"Restore all chats without attachments"**. Click **Preview**. | Dry-run result shows the usual statements/rows/tables line, **plus** a distinct line reading exactly in the form: **"Chats: 1 restored, 0 skipped (already exist)"**. |
| 3 | Re-check Project B's chat count and non-chat-entity state. | **Unchanged from the baseline in step 1** — zero chats, nothing written. Preview-only means nothing was actually applied, despite the dry-run reporting what *would* happen. |

### Expected Final State
A Preview-only restore on a chats-included file correctly reports chat-specific counts, with zero actual data changes.

### Pass/Fail Criteria
**Pass:** Chat-specific line present and numerically correct; Project B's state is provably unchanged afterward.
**Fail:** Missing/incorrect chat-specific line, or any actual data change despite Preview only being checked.
