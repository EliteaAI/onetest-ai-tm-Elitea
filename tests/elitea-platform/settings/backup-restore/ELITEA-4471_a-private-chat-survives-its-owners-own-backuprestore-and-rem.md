---
id: ELITEA-4471
title: "A private chat survives its owner's own backup/restore and remains invisible to a different account in the target project; restoring a backup containing another user's private chat as a non-owner correctly never surfaces it, even though the owner restoring the identical file does see it"
priority: critical
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, privacy, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4471: Private chat ownership: a private chat restores and stays private; a non-owner's restore cannot surface someone else's private chat

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Functional

### Preconditions
- "User A"'s own private project, containing 1 private chat: send the first message **"My private note"**.
  Back this project up with **"All chats without attachments"** — this is "File 1".
- "User B"'s own project (any kind), to be used as a restore target. User B is a different account than User A.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | As **User A**, restore File 1 into a **different** project that User A owns/has restore access to (confirming the 409 mismatch flow from TC-M15 if applicable). | The private chat **"My private note" restores correctly and is visible to User A** in the new project. |
| 2 | As **User B**, open that same new project (if User B has access to view it) or any project User B can restore into. Attempt to see the restored chat from step 1. | User B **cannot see** "My private note" — it remains private to User A only. |
| 3 | As **User B** (not the owner), restore **File 1** directly into one of User B's own projects. | The restore modal correctly shows the chat/attachment counts from File 1 (e.g. "Backup contains 1 chats..."). After a real restore, check User B's project's chat list. | **Zero chats are actually restored** — the private chat belongs to User A, not User B, so it is correctly withheld even though User B is the one running the restore. |
| 4 | As **User A**, restore the **same File 1** into one of User A's own projects (repeat of a similar action to step 1, different target). | The private chat **is correctly restored** — confirms the refusal in step 3 is specifically about ownership, not a general inability to restore this file. |

### Expected Final State
Private chat visibility/ownership rules hold correctly through backup and restore in both directions — an owner's own private chat always comes back for them, and never surfaces for anyone else, regardless of who technically runs the restore action.

### Pass/Fail Criteria
**Pass:** Step 1 and step 4 both correctly restore the private chat for User A; steps 2 and 3 both correctly withhold it from User B.
**Fail:** The private chat ever becoming visible to User B in any step, or failing to restore for User A in steps 1/4.
