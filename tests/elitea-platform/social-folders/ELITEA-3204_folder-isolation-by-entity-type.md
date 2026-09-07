---
id: ELITEA-3204
title: "Folder isolation by entity type"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, entity-type-isolation, folder-scope]
requirements: [EliteaAI/elitea_issues#5194]
---
# ELITEA-3204: Folder Isolation by Entity Type

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify that a folder created and populated for one entity type is not visible or applicable when viewing a different entity type in the same project, and remains correct on the original entity type afterward.

## Entities to Test

Select one source entity type and one different comparison entity type from the list below. Record both selected types with the result; do not imply that every pair was tested unless it was executed.

- Agents
- Skills
- Pipelines
- Toolkits & Indexes
- MCPs
- Credentials

## Steps

| # | Action | Expected Result |
|---|---|---|
| 1 | On the source entity type, create a unique folder and assign an entity to it. | The folder and assignment exist for the source entity type. |
| 2 | Switch to the comparison entity type in the same project. | The folder and assignment are not shown for the comparison entity type. |
| 3 | Switch back to the source entity type. | The folder, its assignment, and count remain unchanged. |

## Expected Final State

The folder created for the source entity type is visible only for that entity type within the project; the comparison entity type shows no trace of it.

## Pass/Fail Criteria

**Pass:**
- The folder and its assignment are visible only for the source entity type.
- The comparison entity type shows no trace of the folder or assignment.
- Returning to the source entity type shows everything unchanged.

**Fail:**
- The folder or assignment is visible for the comparison entity type.
- The folder or assignment is lost or altered when returning to the source entity type.

## Cleanup

Delete the temporary folder created for the source entity type.
