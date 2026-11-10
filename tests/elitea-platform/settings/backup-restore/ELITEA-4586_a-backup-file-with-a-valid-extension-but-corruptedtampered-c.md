---
id: ELITEA-4586
title: "A backup file with a valid extension but corrupted/tampered content is rejected with a clear error and writes no data, verified as its own functional check separate from the known Preview/Restore-button-stays-enabled defect (TC-M18)"
priority: critical
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, security, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4586: Malformed/corrupted backup file (valid extension) is safely rejected, independent of the button-state bug

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Functional

**Note:** this case is deliberately kept separate from **TC-M18** — TC-M18 exists specifically to track the
confirmed button-disable defect; this case exists to verify the rejection-and-no-data-written behavior stands
on its own merits, regardless of that defect's status/fix.

### Preconditions
- Project A: a project with at least 1 Agent and 1 chat (any first message), to clearly observe nothing
  changes. Back up Project A with **"All chats without attachments"**.
- A copy of that backup file with several bytes altered in the middle of the file (not the first bytes, so
  the outer encrypted-envelope header is still intact and the file is still recognized as the right type).
- A second copy of that backup file with bytes altered very close to the start (corrupting the envelope
  header itself).

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Note Project A's current Agent and chat state (baseline). | Baseline recorded. |
| 2 | Upload the mid-file-corrupted copy to "Restore from the Backup" in Project A. Click Preview, then (separately, starting fresh) click Restore directly. | Both attempts are rejected with a clear error (e.g. "Backup file is malformed"). Project A's Agent and chat remain **exactly as the baseline** — nothing written. |
| 3 | Upload the header-corrupted copy instead. Click Restore. | Rejected with a clear error (e.g. "unrecognized backup file"). Project A's state remains unchanged. |

### Expected Final State
Any corruption — whether in the file's content or its header — is safely rejected with a clear error and zero data impact, regardless of exactly where in the file the corruption occurred.

### Pass/Fail Criteria
**Pass:** Both corrupted variants are rejected with a clear error; Project A's state is provably unchanged after each attempt.
**Fail:** Either corrupted file is accepted/partially applied, or any change occurs to Project A's data.

---
