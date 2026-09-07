---
id: ELITEA-3213
title: "Regression: Folder, search, and highlight state persist across Card/Table view changes"
priority: medium
type: regression
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, regression, folder-navigation, view-persistence]
requirements: [EliteaAI/elitea_issues#5194]
---
# ELITEA-3213: Regression - Folder/Search/Highlight State Persistence

**Module:** Social Folders · **Priority:** Medium · **Type:** Regression

**Objective:** Re-verify that an open folder's filter, header, and highlight persist across Card/Table view switches, that search works correctly within an open folder in both views, and that closing the folder leaves a correct folder indicator with tooltip and preserved tags on the entity.

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
| 1 | Open a populated folder in Card view. | Folder filter and header are correct. |
| 2 | Switch to Table view. | Folder, filter, and highlight persist. |
| 3 | Open the Table Actions menu for an entity in the folder. | The current folder is shown checked. |
| 4 | Search within the open folder. | Search works correctly in Table view, respecting folder-agnostic behavior as applicable. |
| 5 | Switch back to Card view. | Folder, filter, and highlight remain correct; search behaves the same as in Table view. |
| 6 | Close the folder. | The entity shows a folder icon with a hover tooltip naming the folder; existing tags remain visible. |

## Expected Final State

The folder filter, header, and highlight remain correct and consistent across view switches; after closing, the entity's folder icon/tooltip and tags are intact.

## Pass/Fail Criteria

**Pass:** Folder state, search behavior, and highlight remain correct and consistent across Card/Table switches; the folder icon, tooltip, and tags are correct after closing.

**Fail:** Any of the folder state, search behavior, highlight, icon, tooltip, or tags is lost, incorrect, or inconsistent between views.

## Cleanup

No data cleanup is required beyond any disposable folder created for setup.
