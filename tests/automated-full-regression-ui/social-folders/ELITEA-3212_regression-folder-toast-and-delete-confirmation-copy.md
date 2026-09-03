---
id: ELITEA-3212
title: "Regression: Folder toast and delete-confirmation copy (#6480)"
priority: high
type: regression
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, issue:6480, regression, toast-copy]
requirements: [EliteaAI/elitea_issues#5194, EliteaAI/elitea_issues#6480]
---
# ELITEA-3212: Regression - Folder Toast and Confirmation Copy

**Module:** Social Folders · **Priority:** High · **Type:** Regression

**Objective:** Re-verify, in one consolidated pass, that every folder-related toast and the delete-confirmation modal show the exact required copy.

## Entities to Test

Execute this case independently for each entity type below. Do not share data or results between rows.

- [ ] Agents
- [ ] Skills
- [ ] Pipelines
- [ ] Toolkits & Indexes
- [ ] MCPs
- [ ] Credentials

## Preconditions

- A unique disposable folder and at least one disposable/recoverable entity are available.
- Record the entity type used.

## Steps

| # | Action | Expected Result |
|---|---|---|
| 1 | Create the folder. | Toast reads exactly: `Folder "[folder name]" has been created.` |
| 2 | Move the entity into the folder. | Toast reads exactly: `"[entity name]" has been moved to "[folder name]".` |
| 3 | Move the entity to a second folder. | Toast reads exactly: `"[entity name]" has been moved to "[second folder name]".` |
| 4 | Remove the entity from the folder. | Toast reads exactly: `"[entity name]" has been removed from "[folder name]".` |
| 5 | Rename the folder. | Toast reads exactly: `Folder has been renamed to "[new folder name]".` |
| 6 | Open the delete confirmation on the folder. | Modal title reads exactly `Delete folder?` and body reads exactly: `[Entity type] in this folder will not be deleted. They will be removed from the folder and remain available in the [Entity type] list.` |
| 7 | Confirm deletion. | Toast reads exactly: `Folder "[folder name]" has been deleted. Its items remain available in the [Entity type] list.` |

## Expected Final State

All toasts and the confirmation modal matched the exact required copy at each step; the folder is deleted and the entity remains available and unfiled.

## Pass/Fail Criteria

**Pass:** Every toast and the confirmation modal text match exactly as specified at each step.

**Fail:** Any toast or the confirmation modal text is missing or does not match exactly.

## Cleanup

Confirm the entity remains available and unfiled; no further cleanup required.
