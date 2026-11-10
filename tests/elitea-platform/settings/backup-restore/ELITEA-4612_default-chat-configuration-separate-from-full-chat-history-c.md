---
id: ELITEA-4612
title: "Default Chat Configuration (separate from full chat history) correctly restores both same-project and cross-project, with cross-project restore only keeping template participants who are actual members of the target project"
priority: high
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, cross-project, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907, EliteaAI/elitea_issues#6788]
---

# ELITEA-4612: Default Chat Configuration survives backup/restore with cross-project membership filtering (extends existing ELITEA-3436 coverage)

**Module:** Project Backup & Restore · **Priority:** High · **Type:** Functional

**Note:** the same-project round-trip half of this (back up → restore → Default Chat Configuration unchanged)
is already covered by the existing case **`ELITEA-3436`** ("Project Backup and Restore Includes Default Chat
Configuration") — this test case does **not** duplicate that; it only adds the cross-project
membership-filtering behavior that `ELITEA-3436` does not exercise, and confirms the setting survives
regardless of which Chats option (#6907's new radio group) is selected.

### Preconditions
- "Project A": a team project with "User A" and "User B" both members. Set its **Default Chat Configuration**
  (Settings → General) to include: 1 Agent (from the project) and both User A and User B as pre-configured
  participants. Back up Project A with **"All chats without attachments"**.
- "Project B": a different team project with **User A as a member but NOT User B**, and with no Default Chat
  Configuration template of its own.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | As User A, restore the Project A backup into Project B (confirming the 409 mismatch flow as needed), with any chat-inclusive option selected. | Restore completes. |
| 2 | Open Project B's Settings → General → Default Chat Configuration. | A template now exists, correctly including the **Agent** and **User A** (both exist/are members of Project B). **User B is correctly NOT included** (not a member of Project B). |
| 3 | Open a new chat in Project B. | The Agent and User A pre-populate as participants; User B does not appear. |

### Expected Final State
Default Chat Configuration restores correctly across projects, filtered by the same membership rules applied to chat participants elsewhere in this epic.

### Pass/Fail Criteria
**Pass:** Template correctly includes only the Agent and User A; new chat pre-population matches.
**Fail:** User B incorrectly included, or the Agent/User A missing from the restored template.
