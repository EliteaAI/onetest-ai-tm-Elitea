---
id: ELITEA-4608
title: "After an entity or chat is edited following a backup, a Merge-mode restore of that backup leaves the live edit untouched, while a Replace-mode restore of the same backup correctly reverts the content back to exactly what was in the backup"
priority: critical
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, data-integrity, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4608: Content fidelity: Merge preserves a live edit; Replace correctly reverts it to the backup's original content (non-chat entity and chat content)

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Functional

### Preconditions
- A project ("Project A") containing: (1) 1 Agent, created via Agents → Create, with its instructions set to
  an exact, known piece of text (note it verbatim); (2) 1 chat — send the first message **"Original wording
  stays here"** (1 message, no follow-up). Back up Project A with **"All chats without attachments"** to
  produce one single test file used for both parts below.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Edit the Agent's instructions, appending **" -EDITED"** to the exact text noted in Preconditions. Rename the chat to **"Edited chat name"**. | Live state: Agent instructions end in "-EDITED"; chat is named "Edited chat name". |
| 2 | Restore the Preconditions' backup into Project A, Preview only unchecked, **Replace unchecked** (merge mode). | Result reports the usual statements/rows (non-chat entities skipped since they already exist, chats skipped too — `Chats: 0 restored, 1 skipped`). Re-check the Agent's instructions and the chat name. | **Both remain exactly as edited** — instructions still end in "-EDITED", chat is still named "Edited chat name". Merge mode never overwrote either. |
| 3 | Restore the **same backup file** again into Project A, this time with **Replace checked**. | Result reports **"Chats: 1 restored, 0 skipped"** (full delete-and-reinsert). Re-check the Agent's instructions and the chat name. | The Agent's instructions **correctly revert** to the exact original text noted in Preconditions (no "-EDITED" suffix). The chat's name **correctly reverts** to being auto-derived from its first message again (i.e. no longer "Edited chat name" — it reflects the backup's original state, not the live edit). The chat's 1 message content is unchanged/correct. |

### Expected Final State
Merge-mode restore never silently overwrites live content that already exists; Replace-mode restore genuinely, correctly reverts both a non-chat entity and a chat back to the exact content captured in the backup.

### Pass/Fail Criteria
**Pass:** Step 2 shows both edits preserved; step 3 shows both edits correctly reverted to the original backup content.
**Fail:** Either edit surviving Replace mode, or either edit being lost/overwritten by Merge mode.
