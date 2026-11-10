---
id: ELITEA-4623
title: "[Regression] Merge-mode restore skips an already-existing chat without duplicating it and preserves live edits; Replace-mode restore deletes all existing chats and replaces them with the backup's exact content"
priority: critical
type: regression
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, regression, data-integrity, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4623: [Regression] Merge preserves existing chats and skips duplicates; Replace deletes and replaces — verified by message content

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Regression

### Preconditions
- A project ("Project A") containing exactly 1 chat: send the first message **"Baseline wording"** (1
  message). Back it up with **"All chats without attachments"**.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Rename the chat to **"Edited name"**. Create a second, unrelated chat with the first message **"Extra chat"**. | 2 chats present: the renamed one, plus the new unrelated one. |
| 2 | Restore the backup, Replace **unchecked** (merge). | **"Chats: 0 restored, 1 skipped"**. Both chats remain exactly as in step 1 — no duplicate, no reversion, "Extra chat" still present. |
| 3 | Restore the **same backup** again. Before clicking Restore, check **Replace existing data - do not merge** and read the warnings shown. | The generic warning reads exactly: **"If checked, the existing rows in the affected tables will be deleted before applying the backup. If unchecked, the existing rows will be preserved and new rows will be merged with them."** The chat-specific warning reads exactly: **"All existing chats in \<Project A's name\> will be permanently deleted and replaced with the chats from the backup."** Both shown together. |
| 4 | Click **Restore**. | **"Chats: 1 restored, 0 skipped"**. Exactly **1 chat** remains, reverted to its original name ("Baseline wording") and original 1-message content; "Extra chat" is gone. |

### Expected Final State
Merge and Replace behave with verifiably opposite, correct outcomes on the same data, and both Replace-mode warnings display correctly together.

### Pass/Fail Criteria
**Pass:** Steps 2-4 all match exactly as described, including both exact warning texts in step 3.
**Fail:** Any duplication, any content not reverting under Replace, "Extra chat" surviving Replace, or either warning text wrong/missing.
