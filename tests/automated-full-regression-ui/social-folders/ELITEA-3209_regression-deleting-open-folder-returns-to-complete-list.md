---
id: ELITEA-3209
title: "Regression: Deleting the currently open folder returns to the complete list (#6484)"
priority: critical
type: regression
module: social-folders
status: ready
execution_type: automated
tags: [feat:social-folders, issue:5194, issue:6484, regression, delete-folder]
requirements: [EliteaAI/elitea_issues#5194, EliteaAI/elitea_issues#6484]
automation_test_id:
  - tests.ui.social_folders.test_deleting_open_folder_returns_complete_list.TestDeletingOpenFolderReturnsCompleteList.test_deleting_open_folder_returns_complete_list
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/2307
---
# ELITEA-3209: Regression - Deleting the Currently Open Folder

**Module:** Social Folders · **Priority:** Critical · **Type:** Regression

**Objective:** Re-verify that deleting a folder while it is open immediately returns the view to the complete unfiltered list, and that its entities remain available and unfiled.

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
| 1 | Create a disposable folder and assign two disposable entities to it. | The folder count matches (2). |
| 2 | Open the folder. | Only its two entities are shown. |
| 3 | Delete the open folder and confirm. | The view immediately returns to the complete unfiltered list. |
| 4 | Inspect the two former entities. | Both remain available and unfiled. |

## Expected Final State

The folder no longer exists; the complete unfiltered list is shown; both entities remain available and unfiled.

## Pass/Fail Criteria

**Pass:** Deleting the open folder immediately restores the complete list and both entities remain available/unfiled.

**Fail:** The view does not return to the complete list, or either entity is missing/altered.

## Cleanup

Confirm both entities remain unfiled; no further action required.
