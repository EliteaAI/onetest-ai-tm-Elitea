---
id: ELITEA-4610
title: "Restoring a backup into a different project than it was taken from requires explicitly confirming the foreign-data warning; chat participants who are members of the target project are kept, participants who are not members are dropped from the live list (without losing their messages), and agents re-link only if they exist in the target project"
priority: critical
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, cross-project, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4610: Cross-project restore: the 409 mismatch gate, and participant re-mapping by membership

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Functional

### Preconditions
- "Project A": a team project with "User A" (the tester) and "User B" (a second account) both as members,
  plus 1 Agent (created via Agents → Create, any distinguishable name).
- In Project A, create 1 chat: send a first message as User A, add **User B** as a participant, add the
  **Agent** as a participant, and have User B also send one message in it. Back up Project A with **"All
  chats without attachments"**.
- "Project B": a different team project that has **User A as a member but does NOT have User B as a member**,
  and does **not** contain an Agent with the same name as Project A's Agent.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | As User A, open "Restore from the Backup" in Project B, upload the Project A backup file. Select any Chats option (e.g. "Restore all chats without attachments"), leave Preview only checked, click Preview. | A warning appears, reading exactly in the form: **"This data was backed up from project \<Project A's id\>. If you restore it to '\<Project B's name\>' (project \<Project B's id\>), you will put foreign data into the project."** A checkbox **"Restore here anyway"** is shown. Preview/Restore stays **disabled** until this checkbox is checked. |
| 2 | Check **"Restore here anyway"**, click Preview, then uncheck Preview only and Restore for real. | Restore completes; result shows the chat restored. |
| 3 | Open the restored chat in Project B. Check its participant list. | **User A** (a Project B member) is present as a participant. **User B** (NOT a Project B member) is **absent from the live participant list**. The **Agent** (which doesn't exist by name in Project B) is also **absent** from the participant list — no crash, no broken placeholder. |
| 4 | Check the chat's message history. | **All messages are still present**, including the message that was originally sent by User B — User B's name still displays correctly as that message's sender, even though User B is not a current participant. No message content or count is lost. |

### Expected Final State
The 409 mismatch gate correctly blocks restore until explicitly confirmed; non-member participants and non-existent-in-target agents are correctly excluded from the live participant list without any loss of message history or author attribution.

### Pass/Fail Criteria
**Pass:** Mismatch warning exact; Preview/Restore gated behind the checkbox; User A present, User B and the Agent absent from participants; all messages present with correct original author attribution.
**Fail:** Missing/wrong warning text, ungated restore, incorrect participant list, or any message lost/misattributed.
