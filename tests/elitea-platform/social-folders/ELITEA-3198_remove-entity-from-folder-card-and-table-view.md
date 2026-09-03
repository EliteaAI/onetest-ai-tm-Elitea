---
id: ELITEA-3198
title: "Remove an entity from a folder from Card and Table view"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, issue:6480, remove-from-folder, folder-count]
requirements: [EliteaAI/elitea_issues#5194, EliteaAI/elitea_issues#6480]
---
# ELITEA-3198: Remove an Entity from a Folder

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify that removing an entity from a folder via Remove from folder, from both Card and Table view, shows the exact removal toast, decrements the folder count by one, unfiles the entity while keeping it visible and searchable, and leaves its configuration, tags, and pin state unchanged.

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
| 1 | Record the folder count and the filed entity's configuration, tags, and pin state. | Baseline is recorded. |
| 2 | From Card view, select Remove from folder. | The toast reads exactly: `"[entity name]" has been removed from "[folder name]".` |
| 3 | Inspect the folder and main list. | Count decreases by 1 immediately; entity is unfiled, remains visible, and appears in search. |
| 4 | Verify entity data. | Configuration, tags, and pin state are unchanged. |
| 5 | Repeat removal from a Table row action using a second filed entity. | The same exact removal toast format appears in Table view: `"[entity name]" has been removed from "[folder name]".` |

## Expected Final State

Both tested entities are unfiled, remain visible in the full list and in search, with configuration, tags, and pin state unchanged; the source folder counts decreased by 1 each.

## Pass/Fail Criteria

**Pass:**
- Toast reads exactly `"[entity name]" has been removed from "[folder name]".` in both Card and Table view.
- Folder count decreases by 1 immediately for each removal.
- The entity becomes unfiled, remains visible, and appears in search.
- Entity configuration, tags, and pin state are unchanged.

**Fail:**
- The toast text is missing or does not match exactly in either view.
- The folder count does not decrease, or decreases incorrectly.
- The entity disappears from the listing/search, or its configuration/tags/pin state changes.

## Cleanup

No folder assignment should remain for the temporary entities.
