---
id: ELITEA-4467
title: "Restoring the same with-attachments backup two ways: 'Restore all chats with attachments' uploads files that open/download correctly; 'Restore all chats without attachments' never uploads, and shows the exact '(file not available)' placeholder for a file the target project doesn't already have"
priority: critical
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4467: Restore attachments: "with attachments" uploads and works; "without attachments" (same backup) never uploads, shows the exact placeholder when the file is missing

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Functional

### Preconditions
- A project ("Project A") containing 1 chat: send the first message **"Here is the file"**, then upload 1
  file as the user (any file, note its exact filename). Back it up with **"All chats with attachments"**.
- A second, brand-new project ("Project B") with zero chats and zero files in its Artifacts bucket, to
  restore into (so it is guaranteed not to already have the file).

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | In Project B, restore the Preconditions' file, Preview only unchecked, Replace unchecked, selecting **"Restore all chats with attachments"**. | Result shows **"Attachments: 1 uploaded, 0 failed"**. Open the restored chat in Project B and click the attachment — it **opens/downloads successfully**. Check Project B's Artifacts bucket — the file now exists there. |
| 2 | Delete this chat from Project B (so it can be restored fresh again). Restore the **same file** again, this time selecting **"Restore all chats without attachments"**. | Result shows **"Attachments: 0 uploaded, 1 failed"** (or an equivalent explicit "not uploaded" indicator — no upload occurs in this mode). Open the restored chat — the attachment message shows exactly the placeholder: **"📎 \<filename\> (file not available)"**, with no working download link. |

### Expected Final State
"With attachments" genuinely uploads and produces a working attachment; "without attachments" never uploads, and correctly shows the file-not-available placeholder when the target has no prior copy of the file.

### Pass/Fail Criteria
**Pass:** Step 1's file opens/downloads correctly; step 2 shows the exact placeholder text with no download link.
**Fail:** Step 1's file fails to open, or step 2 either uploads anyway or shows wrong/missing placeholder text.
