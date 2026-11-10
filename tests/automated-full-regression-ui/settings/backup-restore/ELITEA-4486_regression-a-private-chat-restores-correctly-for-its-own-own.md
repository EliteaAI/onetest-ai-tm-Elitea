---
id: ELITEA-4486
title: "[Regression] A private chat restores correctly for its own owner and stays invisible to a different account; a non-owner cannot surface someone else's private chat even when running the restore themselves"
priority: critical
type: regression
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, privacy, regression, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4486: [Regression] Private chat ownership symmetry holds through restore

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Regression

### Preconditions
- "User A"'s own private project with 1 private chat (any first message). Back it up with **"All chats
  without attachments"**.
- "User B" — a different account with their own project to restore into.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | As User A, restore this backup into a different project User A owns. | The private chat restores and is visible to User A there. |
| 2 | As User B, restore the **same backup file** into one of User B's own projects. | **Zero chats restored** — the chat belongs to User A, not User B, and is correctly withheld. |

### Expected Final State
Ownership-based privacy holds through restore in both directions.

### Pass/Fail Criteria
**Pass:** Both steps match exactly.
**Fail:** The chat becoming visible/restorable for User B, or failing to restore for User A.
