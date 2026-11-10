---
id: ELITEA-4484
title: "[Regression] 'Restore all chats with attachments' uploads a working attachment into a project that never had it; 'Restore all chats without attachments' never uploads and shows the exact file-not-available placeholder"
priority: critical
type: regression
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, regression, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4484: [Regression] Attachment restore: upload-and-open works; non-existent-target shows the exact placeholder

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Regression

### Preconditions
- A project ("Project A") containing 1 chat: send a first message, upload 1 file as the user. Back it up with
  **"All chats with attachments"**.
- A brand-new project ("Project B") with no chats and no matching file in its Artifacts bucket.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Restore into Project B selecting **"Restore all chats with attachments"**. | **"Attachments: 1 uploaded, 0 failed"**; the file opens/downloads from the restored chat; it now exists in Project B's Artifacts bucket. |
| 2 | Delete the chat from Project B. Restore the **same file** again, selecting **"Restore all chats without attachments"**. | **"Attachments: 0 uploaded, 1 failed"** (or equivalent); the restored message shows exactly **"📎 \<filename\> (file not available)"** with no download link. |

### Expected Final State
Both attachment-handling paths behave exactly as specified.

### Pass/Fail Criteria
**Pass:** Both steps match exactly.
**Fail:** Either an unexpected upload in step 2, a broken file in step 1, or wrong placeholder text.
