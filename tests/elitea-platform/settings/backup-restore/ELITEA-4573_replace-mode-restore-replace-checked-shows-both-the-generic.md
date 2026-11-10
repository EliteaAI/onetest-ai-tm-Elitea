---
id: ELITEA-4573
title: "Replace-mode restore (Replace checked) shows both the generic existing-rows warning and the exact chat-specific warning text, then deletes every existing chat in the target project and replaces them with exactly the backup's chats — verified by exact message content"
priority: critical
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4573: Restore (Replace mode): warning text, and existing chats are wholly deleted and replaced (not merged)

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Functional

### Preconditions
- A project ("Project A") containing exactly 1 chat: send the first message **"Original content here"**, then
  one follow-up reply (2 messages total). Back it up with **"All chats without attachments"** to produce the
  test file.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | In Project A, rename this chat to **"Renamed before replace"**. Create a brand-new, second, unrelated chat with the first message **"This one should disappear"**. | Project A now has 2 chats: the renamed original, and the new unrelated one. |
| 2 | Open "Restore from the Backup" in Project A, upload the file from Preconditions. Check **Replace existing data - do not merge**, select **"Restore all chats without attachments"**. Before clicking Restore, read every warning shown. | The generic warning (present since before #6907, for any Replace-mode restore regardless of chats) reads exactly: **"If checked, the existing rows in the affected tables will be deleted before applying the backup. If unchecked, the existing rows will be preserved and new rows will be merged with them."** In addition, a chat-specific warning appears (new for #6907, shown only when Replace is checked AND a chat-inclusive option is selected), reading exactly: **"All existing chats in \<Project A's name\> will be permanently deleted and replaced with the chats from the backup."** Both warnings are visible together. |
| 3 | Uncheck **Preview only** (real restore), click **Restore**. | Result shows **"Chats: 1 restored, 0 skipped (already exist)"** (not "skipped" — everything is deleted and reinserted, not merged). |
| 4 | Check Project A's chat list and open the surviving chat. | Exactly **1 chat** remains. It is named **"Original content here"** (reverted — the rename from step 1 did NOT survive Replace). The unrelated second chat from step 1 is **completely gone**. The chat's 2 messages exactly match the original backup content, in the original order. |

### Expected Final State
Replace mode shows both the generic and the chat-specific warning together, and genuinely performs a full delete-then-reinsert for chats, verified down to exact message content and chat naming — not a merge.

### Pass/Fail Criteria
**Pass:** Both warning texts exact and shown together; exactly 1 chat remains with reverted name and exact original message content; the unrelated chat is gone.
**Fail:** Either warning text wrong/missing, the unrelated chat survives, the rename survives, or message content/count differs from the original backup.
