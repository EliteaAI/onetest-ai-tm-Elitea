---
id: ELITEA-3205
title: "Folder isolation by project"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, project-isolation, folder-scope]
requirements: [EliteaAI/elitea_issues#5194]
---
# ELITEA-3205: Folder Isolation by Project

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify that a folder created and populated in one project is not visible when switching to a different project for the same entity type, and remains correct upon returning to the original project.

## Entities to Test

Execute this case independently for each entity type below, using fresh disposable test data per entity. Do not share data or results between rows.

- [ ] Agents
- [ ] Skills
- [ ] Pipelines
- [ ] Toolkits & Indexes
- [ ] MCPs
- [ ] Credentials

## Preconditions

- Two distinct projects (Project A and Project B) are available, each with at least one entity of the tested type.
- A unique folder name is chosen for this case.

## Steps

| # | Action | Expected Result |
|---|---|---|
| 1 | In Project A, create the unique folder and assign an entity to it. | The folder and assignment exist in Project A. |
| 2 | Switch to Project B for the same entity type. | No trace of the folder or assignment appears in Project B. |
| 3 | Switch back to Project A. | The folder, assignment, and count are intact and unchanged. |

## Expected Final State

The folder is scoped to Project A only; Project B shows no trace of it for the same entity type.

## Pass/Fail Criteria

**Pass:**
- The folder and assignment exist only in Project A.
- Project B shows no trace of the folder or assignment for the same entity type.
- Returning to Project A shows the folder and assignment intact.

**Fail:**
- The folder or assignment appears in Project B.
- The folder or assignment is lost or altered when returning to Project A.

## Cleanup

Delete the temporary folder from Project A.
