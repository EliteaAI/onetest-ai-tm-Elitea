---
id: ELITEA-4458
title: "Selecting 'Do not include chats' (the default) produces the exact same filename pattern and table scope as a backup taken before chat-inclusion existed"
priority: critical
type: functional
module: project-backup-restore
status: draft
execution_type: manual
tags: [feat:backup-restore, backward-compatibility, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6907]
---

# ELITEA-4458: Backup output: "Do not include chats" is byte-for-byte the pre-#6907 baseline

**Module:** Project Backup & Restore · **Priority:** Critical · **Type:** Functional

### Preconditions
- Any project ("Project A") containing at least 1 Agent (created via Agents → Create, any distinguishable
  name/instructions) and at least 1 chat (any first message).

### Steps
| # | Action | Expected Result |
|---|---|---|
| 1 | Open "Create Project Backup", leave the default **"Do not include chats"** selected, click **Backup**. | File downloads. Filename matches exactly: **`elitea-backup-<project id>-<project slug>-safe-<YYYY-MM-DD>-<HH-mm-ss>.sql.enc`** (no `-chats-` segment anywhere in the name). |
| 2 | Upload this same file to "Restore from the Backup" on any project, with **Preview only** checked. Click Preview. | Dry-run summary reports only non-chat tables/rows (Agent and any other project entities) — **no chat-related line anywhere** in the result, and no `Chats:` count appears at all (distinct from a chat-inclusive file's result — see TC-M09/TC-M10). |

### Expected Final State
The default, backward-compatible backup option produces output indistinguishable in structure from a pre-#6907 backup — no chat data, no chat-specific filename segment, no chat-specific restore-summary line.

### Pass/Fail Criteria
**Pass:** Filename pattern exact; restore dry-run shows zero chat-related content.
**Fail:** Any `-chats-` segment in the filename, or any chat-related line appearing in the dry-run summary.
