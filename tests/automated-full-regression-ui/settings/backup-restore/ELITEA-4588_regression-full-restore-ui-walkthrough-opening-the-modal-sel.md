---
id: ELITEA-4588
title: "[Regression] Full Restore UI walkthrough — opening the modal, selecting a file, confirming the Chats block reflects that file's content, running a real restore, and verifying the result summary"
priority: critical
type: regression
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, regression, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4588: [Regression] Restore from the Backup: full E2E UI walkthrough, file-dependent Chats options, and the result summary

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Regression

### Preconditions
- A project ("Project A") containing 1 chat: send a first message, then upload 1 file as the user. Back it up
  with **"All chats with attachments"** — this is the file used below.
- A second, brand-new project ("Project B") with zero chats, to restore into.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | In Project B, click **"Restore from the Backup"**. | Modal "Restore Project Data" opens, showing the description text with Project B's name, **"Choose a backup file"**, **"Preview only (no data is restored yet)"** checked by default, **"Replace existing data - do not merge"** unchecked, Cancel/Preview buttons. |
| 2 | Click "Choose a backup file", select the Preconditions' file. | Filename and size shown. A **Chats** block appears: all 3 restore options enabled (file has attachments), default selection **"Restore all chats with attachments"**, info line **"Backup contains 1 chats · 1 attachments (~\<size\>)"**. |
| 3 | Leave Preview only checked, click **Preview**. | Dry-run result shown with statements/rows/tables plus **"Chats: 1 restored, 0 skipped"**; nothing written yet (confirm Project B's chat count is still 0). |
| 4 | Uncheck **Preview only**, click **Restore**. | Real restore runs; button shows a loading state during the request. Result summary shown, reading in the form: **"Chats: 1 restored, 0 skipped (already exist) · Attachments: 1 uploaded, 0 failed"**, alongside the existing statements/rows/tables line. |
| 5 | Check Project B's chat list and the restored attachment. | The chat now exists in Project B with its 1 message intact; the attachment opens/downloads correctly. |

### Expected Final State
The full Restore UI path — modal open, file-dependent Chats block, Preview dry run, real restore, and the result summary — works correctly end to end.

### Pass/Fail Criteria
**Pass:** Modal text/defaults exact; Chats block correctly reflects the uploaded file; Preview writes nothing; real restore's result summary matches exactly; the chat and attachment are genuinely restored and functional.
**Fail:** Any text/default mismatch, Chats block not reflecting the file's real content, Preview writing data, wrong/missing result summary line, or a broken/missing chat or attachment after restore.
