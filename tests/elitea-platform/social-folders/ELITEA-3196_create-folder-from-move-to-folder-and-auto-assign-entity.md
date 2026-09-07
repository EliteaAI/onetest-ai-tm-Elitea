---
id: ELITEA-3196
title: "Create a folder from Move-to-folder and auto-assign the initiating entity"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, issue:6480, create-folder, move-entity]
requirements: [EliteaAI/elitea_issues#5194, EliteaAI/elitea_issues#6480]
---
# ELITEA-3196: Create a Folder from Move to Folder

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify that Create Folder is reachable from the Move to folder menu for an unfiled entity, and that creating a folder this way automatically assigns the initiating entity to the new folder, with exact creation and move toasts, from both Card and Table view.

## Entities to Test

Execute this case independently for each entity type below, using fresh disposable test data per entity. Do not share data or results between rows.

- [ ] Agents
- [ ] Skills
- [ ] Pipelines
- [ ] Toolkits & Indexes
- [ ] MCPs
- [ ] Credentials

## Steps

| # | Action | Expected Result |
|---|---|---|
| 1 | From an unfiled entity Card action, open Move to folder. | Create Folder is available; Remove from folder is not shown. |
| 2 | Select Create Folder, enter a unique folder name, and save. | The toasts read exactly: `Folder "[folder name]" has been created.` and `"[entity name]" has been moved to "[folder name]".` |
| 3 | Reopen Move to folder. | The new folder is checked and the entity is assigned exactly once. |
| 4 | Repeat from a Table row action with another unfiled entity, creating another unique folder. | The toasts read exactly: `Folder "[new folder name]" has been created.` and `"[entity name]" has been moved to "[new folder name]".` |

## Expected Final State

A new folder exists per creation attempt, each containing exactly the entity that initiated its creation; no Remove-from-folder option was available before the entity had a folder assignment.

## Pass/Fail Criteria

**Pass:**
- Create Folder is available from Move to folder for an unfiled entity; Remove from folder is not shown.
- Both toasts appear and read exactly as specified for folder creation and entity move, in both Card and Table view flows.
- Reopening Move to folder shows the new folder checked with the entity assigned exactly once.

**Fail:**
- Create Folder is unavailable, or Remove from folder is shown for an unfiled entity.
- Either toast is missing or does not match the exact copy.
- The new folder is not checked, or the entity is assigned more than once.

## Cleanup

Delete the temporary folder. Confirm both initiating entities remain available and unfiled.
