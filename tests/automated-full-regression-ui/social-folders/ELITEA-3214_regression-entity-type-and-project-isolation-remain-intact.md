---
id: ELITEA-3214
title: "Regression: Entity-type and project isolation remain intact"
priority: medium
type: regression
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, regression, folder-scope, isolation]
requirements: [EliteaAI/elitea_issues#5194]
---
# ELITEA-3214: Regression - Entity-Type and Project Isolation

**Module:** Social Folders · **Priority:** Medium · **Type:** Regression

**Objective:** Re-verify, in one consolidated pass, that a folder created for one entity type in one project is not visible from a different entity type in the same project, nor from the source entity type in a different project.

## Entities to Test

Select one source entity type and one different comparison entity type from the list below. Also select two distinct projects (source project and comparison project). Record the source entity type, comparison entity type, and both projects with the result.

- Agents
- Skills
- Pipelines
- Toolkits & Indexes
- MCPs
- Credentials

## Preconditions

- A unique disposable folder name is chosen for this case.

## Steps

| # | Action | Expected Result |
|---|---|---|
| 1 | In the source project, on the source entity type, create the folder and assign an entity to it. | The folder and assignment exist for the source entity type in the source project. |
| 2 | In the source project, switch to the comparison entity type. | The folder and assignment are not visible. |
| 3 | Switch to the comparison project, then to the source entity type. | The folder and assignment are not visible. |
| 4 | Return to the source project and source entity type. | The folder, assignment, and count are unchanged. |

## Expected Final State

The folder remains visible only under its original project/entity-type combination.

## Pass/Fail Criteria

**Pass:** The folder is visible only for the source project/entity-type combination and is unchanged upon return.

**Fail:** The folder or assignment is visible in the comparison entity type or comparison project, or is altered upon return.

## Cleanup

Delete the temporary folder from the source project.
