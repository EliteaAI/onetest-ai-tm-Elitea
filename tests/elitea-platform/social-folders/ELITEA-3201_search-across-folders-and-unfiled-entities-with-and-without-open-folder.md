---
id: ELITEA-3201
title: "Search across folders and unfiled entities with and without an open folder"
priority: medium
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, search, folder-indicator]
requirements: [EliteaAI/elitea_issues#5194]
---
# ELITEA-3201: Search Across Folders and Unfiled Entities

**Module:** Social Folders · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that search returns matches regardless of folder assignment when no folder is selected, remains folder-agnostic while a different folder is open, and that clearing search restores the prior list context.

## Entities to Test

Execute this case independently for each entity type below, using fresh disposable test data per entity. Do not share data or results between rows.

- [ ] Agents
- [ ] Skills
- [ ] Pipelines
- [ ] Toolkits & Indexes
- [ ] MCPs
- [ ] Credentials

## Test Data

| Entity | Folder assignment |
|---|---|
| Entity A | Filed in Folder 1 |
| Entity B | Filed in Folder 2 |
| Entity C | Unfiled |

## Steps

| # | Action | Expected Result |
|---|---|---|
| 1 | With no folder selected, search for a term matching Entity A, B, and C. | All three appear regardless of folder assignment; filed entities show their folder association, unfiled entities do not. |
| 2 | Open Folder 1, then search for a term matching Entity B or Entity C. | Entity B and/or Entity C still appear in results despite not being in Folder 1 (search is folder-agnostic). |
| 3 | Clear the search. | The prior list context (the previously open folder or complete list) is restored. |

## Expected Final State

Search results are not restricted by the currently open folder; clearing search returns the view to its prior context.

## Pass/Fail Criteria

**Pass:**
- Search with no folder selected returns matches regardless of folder assignment, showing folder association only for filed entities.
- Search while a different folder is open still returns matches from other folders/unfiled entities.
- Clearing search restores the prior list context.

**Fail:**
- Search results are restricted to the currently open folder.
- Folder association is shown incorrectly or missing for filed entities.
- Clearing search does not restore the prior context.

## Cleanup

No data cleanup is required.
