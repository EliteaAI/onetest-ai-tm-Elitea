---
id: ELITEA-4589
title: "[Regression] Selecting 'Do not restore chats' on a chats-included backup restores only non-chat data, leaving every existing chat in the target project byte-for-byte unchanged"
priority: critical
type: regression
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, regression, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4589: [Regression] "Do not restore chats" leaves existing chats completely untouched

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Regression

### Preconditions
- A project ("Project A") containing 1 chat: send the first message **"Don't touch me"**, then one follow-up
  reply (2 messages total). Back it up with **"All chats without attachments"**.

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Restore this backup into Project A itself, Preview only unchecked, Replace unchecked, selecting **"Do not restore chats"**. | Non-chat data restores normally; no `Chats: ... restored` line appears (or shows explicitly 0 affected). |
| 2 | Check the chat "Don't touch me". | **Byte-for-byte unchanged** — still exactly 2 messages, same content, same order, as before this restore ran. |

### Expected Final State
"Do not restore chats" never touches any existing chat, regardless of what the uploaded file contains.

### Pass/Fail Criteria
**Pass:** The chat is provably unchanged after the restore.
**Fail:** Any change to the chat's content, messages, or existence.
