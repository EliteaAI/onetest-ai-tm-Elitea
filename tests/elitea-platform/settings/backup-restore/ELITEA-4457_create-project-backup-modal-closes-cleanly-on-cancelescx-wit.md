---
id: ELITEA-4457
title: "Create Project Backup modal closes cleanly on Cancel/Esc/X without downloading anything, and the Backup button shows a disabled 'Preparing...' state while the request is in flight"
priority: high
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4457: Create Backup modal: Cancel, Esc, X, and the in-flight "Preparing..." state

**Module:** Project Backup & Restore · **Priority:** High · **Type:** Functional

### Preconditions
- Any project ("Project A") the tester has backup permission on, in any chat state.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Open "Create Project Backup". Select any Chats option. Click **Cancel**. | Modal closes. **Nothing is downloaded.** No backup request is sent (confirm via DevTools Network tab — zero `project_backup` calls). |
| 2 | Reopen the modal. Select any Chats option. Press **Esc**. | Modal closes identically to Cancel — nothing downloaded. |
| 3 | Reopen the modal. Select any Chats option. Click the **✕** close icon. | Modal closes identically to Cancel — nothing downloaded. |
| 4 | Reopen the modal, leave the default selection, click **Backup**. While the request is in flight, observe the button. | Button label changes to **"Preparing..."** and becomes **disabled** for the duration of the request. Attempting to press Esc or click ✕ **while "Preparing..." is showing has no effect** — the modal cannot be closed mid-request. |
| 5 | Wait for completion. | File downloads; toast **"Backup downloaded."** appears; button reverts to its normal "Backup" label and re-enables (modal itself closes after the download starts). |

### Expected Final State
All three cancel paths are clean and download nothing; the modal is un-closeable only during the specific window the backup request is actually running.

### Pass/Fail Criteria
**Pass:** All 5 steps match exactly.
**Fail:** Any cancel path leaving a download behind, or the modal becoming closeable while "Preparing..." is shown.
