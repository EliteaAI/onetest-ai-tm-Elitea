---
id: ELITEA-3206
title: "Folder scope boundaries: no nesting, bulk assignment, or detail-view assignment"
priority: medium
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, scope-boundary, no-nesting]
requirements: [EliteaAI/elitea_issues#5194]
---
# ELITEA-3206: Folder Scope Boundaries

**Module:** Social Folders · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the feature does not support nested subfolders, bulk folder assignment from multi-select, or folder assignment controls in the entity detail/edit view.

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
| 1 | Open an existing folder and look for a Create subfolder or nested-folder action. | No such action is available inside a folder. |
| 2 | Use the top-level Create action. | Only a top-level folder is created; there is no option to nest it under another folder. |
| 3 | Select multiple entities via multi-select and inspect available bulk actions. | No bulk Move to folder action is available. |
| 4 | Open an entity's detail/edit view. | No folder assignment control is present in that view. |

## Expected Final State

No nested folders, bulk folder assignment, or detail-view folder assignment exist anywhere in the tested entity type.

## Pass/Fail Criteria

**Pass:**
- No subfolder/nested-folder creation action exists inside a folder.
- The top-level Create action only creates top-level folders.
- No bulk Move to folder action is available in multi-select.
- No folder assignment control appears in the entity detail/edit view.

**Fail:**
- A subfolder/nesting action is found anywhere.
- Bulk folder assignment is available from multi-select.
- A folder assignment control appears in the detail/edit view.

## Cleanup

No data cleanup is required; this case does not create any folders or assignments.
