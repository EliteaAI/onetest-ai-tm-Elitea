---
id: ELITEA-3436
title: "Project Backup and Restore Includes Default Chat Configuration"
priority: low
type: functional
module: chat
status: draft
execution_type: manual
tags: [feat:chat, feat:project-setup, story:6358, default-chat-config, backup-restore]
requirements: [EliteaAI/elitea_issues#6358]
---
# ELITEA-3436: Project Backup and Restore Includes Default Chat Configuration

**Module:** Chat · **Priority:** Low · **Type:** Functional

**Objective:** Confirm that backing up a project includes its "Default Chat Configuration" (`chat_config.participants`), and restoring from that backup correctly reinstates the same preconfigured participants.

**Coverage:** AC — project-level config should travel with the rest of the project's backed-up state.

## Preconditions

- Admin access to Project Settings → "Back Up & Restore"
- A project with 2+ preconfigured participants configured (mix of agent and pipeline)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm the current "Default Chat Configuration" list and note its contents. | Baseline recorded. |
| 2 | Back up the project via "Back Up & Restore". | Backup completes successfully. |
| 3 | Restore the project from that backup (into the same project, or a new one, depending on what the restore flow supports). | Restore completes successfully. |
| 4 | Open Project Settings → "Default Chat Configuration" on the restored project. | The preconfigured participants list matches the baseline from step 1 — same agents/pipelines, correctly resolved (not broken/stale references). |
| 5 | Open a new chat on the restored project. | Participants pre-populate correctly from the restored configuration. |

## Expected Final State

"Default Chat Configuration" is included in project backup/restore and comes back correctly resolved, not lost or corrupted.

## Pass/Fail Criteria

**Pass:**
- Step 4 matches the pre-backup baseline
- Step 5 shows correct pre-population post-restore

**Fail:**
- The restored project has an empty or broken "Default Chat Configuration" (setting was not included in backup, or restore did not reapply it)
