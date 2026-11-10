---
id: ELITEA-4462
title: "Restore modal's file picker accepts .zip in addition to .enc/.sql, and the Chats option block's visibility, enabled/disabled options, and default selection correctly depend on what the uploaded backup file actually contains"
priority: critical
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4462: Restore modal: file-type acceptance and the Chats block's 3 content-dependent states

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Functional

### Preconditions
- A project ("Project A") used to produce 3 backup files ahead of time:
  - **File 1:** back up Project A with **"Do not include chats"** selected.
  - **File 2:** in Project A, create 1 chat (any first message, no attachment), then back up with **"All
    chats without attachments"** selected.
  - **File 3:** in Project A, create 1 chat (any first message), upload 1 file as the user in it, then back
    up with **"All chats with attachments"** selected.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Open "Restore from the Backup" on any project. Open the native file picker. Confirm a `.zip.enc` file (File 3) is actually selectable, not filtered out by the dialog. | `.zip.enc` is selectable (in addition to the existing `.enc`/`.sql` support). |
| 2 | Upload **File 1**. | No Chats block is shown at all. Info text reads exactly: **"This backup does not contain chats."** The rest of the modal (Preview only checked by default, Replace unchecked by default, Cancel/Preview buttons) is unchanged from before #6907. |
| 3 | Clear and upload **File 2** instead. | A **Chats** block appears with: **"Do not restore chats"**, **"Restore all chats without attachments"** (both selectable) and **"Restore all chats with attachments"** shown **disabled**, tooltip **"This backup has no attachment files"**. Default selection: **"Restore all chats without attachments"**. An info line reads **"Backup contains 1 chats · 0 attachments"**. |
| 4 | Clear and upload **File 3** instead. | All three Chats options are now enabled. Default selection: **"Restore all chats with attachments"**. Info line reads **"Backup contains 1 chats · 1 attachments (~\<size\>)"**. |

### Expected Final State
The Restore modal's Chats block correctly reflects exactly what each specific uploaded file contains, with the correct default in each of the 3 cases.

### Pass/Fail Criteria
**Pass:** All 4 steps match exactly for all 3 files.
**Fail:** Wrong block visibility, wrong enabled/disabled state, wrong default, or `.zip` not selectable in the picker.
