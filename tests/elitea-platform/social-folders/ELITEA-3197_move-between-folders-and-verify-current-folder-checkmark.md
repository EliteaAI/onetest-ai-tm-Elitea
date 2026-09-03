---
id: ELITEA-3197
title: "Move between folders and verify current-folder checkmark"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, issue:6480, move-entity, folder-count]
requirements: [EliteaAI/elitea_issues#5194, EliteaAI/elitea_issues#6480]
---
# ELITEA-3197: Move Between Folders and Checkmark Verification

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify that Move to folder shows a checkmark on an entity's current folder, that moving to a different folder updates both folders' counts by exactly one and updates the checkmark, that reselecting the current folder is a no-op, and that the entity's pin status is unaffected.

## Entities to Test

Execute this case independently for each entity type below, using fresh disposable test data per entity. Do not share data or results between rows.

- [ ] Agents
- [ ] Skills
- [ ] Pipelines
- [ ] Toolkits & Indexes
- [ ] MCPs
- [ ] Credentials

## Preconditions

- Record the entity's pin status before moving.

## Steps

| # | Action | Expected Result |
|---|---|---|
| 1 | Open Move to folder for an entity currently assigned to a folder. | The current folder has the checkmark; Remove from folder is available. |
| 2 | Move the entity to a different existing folder. | The toast reads exactly: `"[entity name]" has been moved to "[new folder name]".` The original folder decreases by 1 and the new folder increases by 1. |
| 3 | Reopen the menu. | Only the new folder has the checkmark. |
| 4 | Select the current folder again. | No update occurs: no assignment duplication, no count change, and no move toast. |
| 5 | Inspect the entity's pin status after the move. | The pin status is unchanged from the recorded baseline. |

## Expected Final State

The entity is assigned to only one folder at a time; the two folders' counts reflect exactly one decrement and one increment; no duplicate move occurs when the current folder is reselected; the entity's pin status remains unchanged throughout.

## Pass/Fail Criteria

**Pass:**
- The current folder shows a checkmark and Remove from folder is available before the move.
- Moving to a different folder shows the exact toast and updates both folder counts by exactly 1 in the correct direction.
- Reopening the menu shows only the new folder checked.
- Reselecting the current folder produces no toast, no count change, and no duplicate assignment.
- The entity's pin status remains unchanged after the move.

**Fail:**
- The checkmark is on the wrong folder, missing, or shown on more than one folder.
- The toast text is wrong/missing, or either folder's count is incorrect.
- Reselecting the current folder triggers a toast, a count change, or a duplicate assignment.
- The entity's pin status changes as a result of the move.

## Cleanup

Return the entity to its original state or remove it from its temporary folder.
