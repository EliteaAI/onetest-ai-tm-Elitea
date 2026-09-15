---
id: ELITEA-3208
title: "Regression: Closing an empty folder returns to the complete list (#6483)"
priority: critical
type: regression
module: social-folders
status: ready
execution_type: automated
tags: [feat:social-folders, issue:5194, issue:6483, regression, empty-folder]
requirements: [EliteaAI/elitea_issues#5194, EliteaAI/elitea_issues#6483]
automation_test_id:
  - tests.ui.social_folders.test_closing_empty_folder_returns_complete_list.TestClosingEmptyFolderReturnsCompleteList.test_closing_empty_folder_returns_complete_list
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/2307
---
# ELITEA-3208: Regression - Closing an Empty Folder

**Module:** Social Folders · **Priority:** Critical · **Type:** Regression

**Objective:** Re-verify that opening an empty folder shows the exact empty message and zero count, and that closing it restores the complete unfiltered list.

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
| 1 | Create a disposable empty folder. | The folder exists with a count of `(0)`. |
| 2 | Open the empty folder. | The panel reads exactly `No items in this folder yet.` with count `(0)`. |
| 3 | Close the folder. | The complete unfiltered list is shown immediately. |

## Expected Final State

The complete unfiltered list is displayed after closing the empty folder.

## Pass/Fail Criteria

**Pass:** The empty-state text and count are exact, and closing restores the complete list immediately.

**Fail:** The empty-state text/count is wrong, or closing fails to restore the complete list.

## Cleanup

Delete the disposable folder.
