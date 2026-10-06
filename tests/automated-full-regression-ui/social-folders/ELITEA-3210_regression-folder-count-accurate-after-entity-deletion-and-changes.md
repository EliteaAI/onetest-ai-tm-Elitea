---
id: ELITEA-3210
title: "Regression: Folder count remains accurate after entity deletion and subsequent changes (#6482)"
priority: critical
type: regression
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, issue:6482, regression, folder-count]
requirements: [EliteaAI/elitea_issues#5194, EliteaAI/elitea_issues#6482]
---
# ELITEA-3210: Regression - Folder Count Accuracy

**Module:** Social Folders · **Priority:** Critical · **Type:** Regression

**Objective:** Re-verify that a folder's item count updates immediately and accurately after an entity is deleted from within the folder, and continues to track correctly through subsequent add/remove operations.

## Entities to Test

Execute this case independently for each entity type below. Do not share data or results between rows.

- [ ] Agents
- [ ] Skills
- [ ] Pipelines
- [ ] Toolkits & Indexes
- [ ] MCPs
- [ ] Credentials

## Steps

| # | Action | Expected Result |
|---|---|---|
| 1 | Assign three disposable entities to a disposable folder. | Count shows `(3)`. |
| 2 | From inside the folder, delete one entity via the normal entity delete action. | Count immediately updates from 3 to 2 without a manual refresh. |
| 3 | Close and reopen the folder. | Count still shows `(2)`. |
| 4 | Add one more entity to the folder. | Count updates from 2 to 3. |
| 5 | Remove one entity from the folder. | Count updates from 3 to 2, with no drift. |

## Expected Final State

The folder count accurately reflects two remaining entities with no drift across the sequence of operations.

## Pass/Fail Criteria

**Pass:** The count updates immediately and correctly after each operation, with no drift or stale values.

**Fail:** The count fails to update immediately, requires a refresh, or drifts from the actual number of entities.

## Cleanup

Delete the disposable folder and any remaining disposable entities.
