---
id: ELITEA-4466
title: "Selecting 'Do not restore chats' on a chats-included backup restores only non-chat data; the target project's existing chats are provably identical before and after"
priority: critical
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4466: Restore: "Do not restore chats" leaves existing chats completely untouched while non-chat data still restores

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Functional

### Preconditions
- A project ("Project A") containing 1 Agent (created via Agents → Create, any distinguishable name/
  instructions) and 1 chat (send the first message **"Don't touch me"**, then one follow-up reply). Back it
  up with **"All chats without attachments"** to produce the test file.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | In Project A, rename the Agent to something different and note its current chat (unchanged, still present). | Baseline: Agent renamed, chat "Don't touch me" still present with its original 2 messages. |
| 2 | Restore the Preconditions' backup into Project A, Preview only unchecked, Replace unchecked, **"Do not restore chats"** selected. | Result shows non-chat statements/rows applied; no `Chats:` restored/skipped line appears at all (or shows explicitly 0 affected, depending on UI — confirm which). |
| 3 | Check the Agent's name and the chat "Don't touch me" in Project A. | The Agent's non-chat data restores per the normal (non-chat) rules (e.g. its rename may or may not revert depending on Merge/Replace for non-chat tables — not the focus here). **The chat "Don't touch me" is byte-for-byte unchanged** — same 2 messages, same content, same order, exactly as it was before this restore. |

### Expected Final State
"Do not restore chats" never touches any existing chat, regardless of what the uploaded backup file contains for chats.

### Pass/Fail Criteria
**Pass:** The chat is provably unchanged (same message count/content/order) after the restore.
**Fail:** Any change to the chat's content, messages, or existence.
