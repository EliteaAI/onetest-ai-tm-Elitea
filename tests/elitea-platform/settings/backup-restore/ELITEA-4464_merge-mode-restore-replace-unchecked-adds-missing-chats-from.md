---
id: ELITEA-4464
title: "Merge-mode restore (Replace unchecked) adds missing chats from the backup while skipping — never duplicating — a chat that already exists in the target project, verified by exact message count/content after the restore"
priority: critical
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4464: Restore (Merge mode): chats are added alongside existing ones; a chat that already exists is skipped, not duplicated

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Functional

### Preconditions
- A project ("Project A") containing exactly 2 chats: Chat 1 — send the first message **"Keep this one"**,
  then send one follow-up reply (2 messages total). Chat 2 — send the first message **"Delete this one
  later"**, then send one follow-up reply (2 messages total). Back up Project A with **"All chats without
  attachments"** to produce the test file.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Delete Chat 2 ("Delete this one later") from Project A, leaving only Chat 1. | Project A now has exactly 1 chat (Chat 1, 2 messages). |
| 2 | Restore the backup file from Preconditions into Project A itself, with **Preview only unchecked** (real restore) and **Replace existing data - do not merge unchecked** (merge mode). Select **"Restore all chats without attachments"**. Click **Restore**. | Result shows **"Chats: 1 restored, 1 skipped (already exist)"** — Chat 2 is restored (it was missing), Chat 1 is correctly skipped (same unique key, already exists) rather than duplicated. |
| 3 | Check Project A's chat list. | Exactly 2 chats present: Chat 1 (unchanged, still exactly 2 messages, same content) and Chat 2 (restored, exactly 2 messages, matching its original content and order). No duplicate of either chat exists. |

### Expected Final State
Merge mode adds back a missing chat and correctly skips (never duplicates) one that already exists, with message count/content verified correct on both.

### Pass/Fail Criteria
**Pass:** Exactly 2 chats after restore, no duplicates, both chats' message counts/content/order correct.
**Fail:** A duplicate of Chat 1 appears, Chat 2 doesn't come back, or any message count/content mismatch.
