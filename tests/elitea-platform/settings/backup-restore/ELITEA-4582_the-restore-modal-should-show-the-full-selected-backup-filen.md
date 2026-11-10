---
id: ELITEA-4582
title: "The Restore modal should show the full selected backup filename (or expose it via hover tooltip) so same-project backups can be told apart by their timestamp; currently the name is truncated with no way to see the full text (confirmed defect, P2 fix targeted for R-2.0.9)"
priority: low
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, bug, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4582: Known defect: Restore modal truncates the selected filename, hiding the distinguishing timestamp

**Module:** Project Backup & Restore · **Priority:** Low · **Type:** Functional

### Preconditions
- 2 backup files of the same project, taken at different times (so they share an identical prefix and differ
  only in their trailing timestamp), e.g. by backing the same project up twice a few minutes apart with the
  same Chats option selected both times.

### Steps
| # | Action | Expected Result (intended/correct behavior) | Actual current behavior (confirmed defect) |
|---|---|---|---|
| 1 | Open "Restore from the Backup", select one of the 2 near-identical-named files. | The full filename — including the distinguishing trailing timestamp — **should be fully visible**, either directly or via a hover tooltip. | **Confirmed defect:** the displayed filename is **truncated**, with no `title`/tooltip attribute exposing the full name on hover — making it impossible to tell which of the 2 near-identical files was actually selected without renaming it first. |

### Expected Final State
Selecting between visually-similar backup files should never require guessing which one was actually chosen. Known, confirmed low-priority defect — not yet filed as of this writing, agreed as P2 for R-2.0.9.

### Pass/Fail Criteria
**Pass (once fixed):** Full filename visible directly or via tooltip.
**Current status:** Fails (tracked defect, not blocking — accepted as a known P2 gap for R-2.0.9). Re-run after the R-2.0.9 fix lands and expect a full Pass.
