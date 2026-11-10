---
id: ELITEA-4613
title: "A malformed or unrecognized backup file is safely rejected with no data written; the Restore/Preview button should disable until a different file is chosen (confirmed defect — currently stays enabled, P2 fix targeted for R-2.0.9)"
priority: low
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, bug, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4613: Known defect: Restore/Preview button stays enabled after a malformed/unrecognized backup file is rejected

**Module:** Project Backup & Restore · **Priority:** Low · **Type:** Functional

### Preconditions
- Any valid backup file (any chat option). A copy of it with a handful of bytes altered somewhere in the
  middle of the file (not the very first bytes, so the outer envelope header is still intact).

### Steps
| # | Action | Expected Result (intended/correct behavior) | Actual current behavior (confirmed defect) |
|---|---|---|---|
| 1 | Upload the tampered copy to "Restore from the Backup" on any project. Click Preview or Restore. | An error is shown (e.g. "unrecognized backup file" / "Backup file is malformed"); **no data is written**. | Matches — error shown correctly, nothing written. |
| 2 | After the error appears, check the state of the **Preview**/**Restore** button. | The button **should become disabled** until a different (valid) file is selected, preventing a pointless retry on a file that will always fail identically. | **Confirmed defect:** the button **remains enabled**, allowing repeated clicks on the same invalid file (each click safely fails again — no actual data risk, purely a UX gap). |

### Expected Final State
File rejection is always safe (no data written either way). The button-disable behavior is a known, confirmed low-priority defect — not yet filed as of this writing, agreed as P2 for R-2.0.9.

### Pass/Fail Criteria
**Pass (once fixed):** Button disables after rejection.
**Current status:** Fails the button-disable expectation (tracked defect, not blocking — accepted as a known P2 gap for R-2.0.9). Re-run after the R-2.0.9 fix lands and expect a full Pass.
