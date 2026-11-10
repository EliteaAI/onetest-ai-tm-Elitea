---
id: ELITEA-4593
title: "[Regression] Cross-project restore is gated behind the foreign-data confirmation checkbox; participants who are not members of the target project are dropped from the live list without losing their message history or author attribution"
priority: critical
type: regression
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, cross-project, regression, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4593: [Regression] Cross-project restore: 409 mismatch gate and participant/author re-mapping by membership

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Regression

### Preconditions
- "Project A": team project with "User A" and "User B" as members. 1 chat: User A sends a message, adds User
  B as a participant, User B sends a message. Back up with **"All chats without attachments"**.
- "Project B": a different team project with User A as a member, **without** User B.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | As User A, upload the backup into Project B's Restore modal. | Mismatch warning shown exactly (project ids/names substituted correctly); Preview/Restore disabled until **"Restore here anyway"** is checked. |
| 2 | Check it, complete a real restore selecting any chat option. | Restore completes; chat appears in Project B. |
| 3 | Check the participant list and message history. | User A present as participant; User B **absent** from participants but User B's **message is still present**, correctly attributed to User B by name. |

### Expected Final State
The gate and the re-mapping rule both hold.

### Pass/Fail Criteria
**Pass:** Both steps 1-3 match exactly.
**Fail:** Ungated restore, missing warning text, lost message, or incorrect author attribution.
