---
id: ELITEA-3193
title: "Create Folder validation, focus, trimming, duplicate names, and exact creation toast"
priority: critical
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, issue:6480, issue:6485, create-folder, duplicate-name]
requirements: [EliteaAI/elitea_issues#5194, EliteaAI/elitea_issues#6475, EliteaAI/elitea_issues#6480, EliteaAI/elitea_issues#6485]
---
# ELITEA-3193: Create Folder Validation, Focus, Trimming, and Toast

**Module:** Social Folders · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Create Folder auto-focuses the Folder Name input, blocks empty/whitespace-only submission, trims leading/trailing whitespace from valid names, allows duplicate (including case-variant) folder names, and shows the exact creation toast copy.

## Entities to Test

Execute this case independently for each entity type below, using fresh disposable test data per entity. Do not share data or results between rows.

- [ ] Agents
- [ ] Skills
- [ ] Pipelines
- [ ] Toolkits & Indexes
- [ ] MCPs
- [ ] Credentials

## Test Data

| Field | Value |
|---|---|
| Temporary folder name | a unique name such as `SF-Create-001` |
| Duplicate folder name | an existing folder with a known name |
| Whitespace input | three spaces |
| Padded input | a unique folder name with leading and trailing spaces |

## Steps

| # | Action | Expected Result |
|---|---|---|
| 1 | Open Create Folder from `+`. Without clicking the input, type a unique folder name. | The Folder Name input has focus on open and receives the text immediately. |
| 2 | Clear the input. | Save is disabled or submission is blocked. |
| 3 | Enter only spaces. | Save remains disabled or submission is blocked; no folder is created. |
| 4 | Enter a name with leading and trailing spaces and save. | A folder with the trimmed name is created. The toast reads exactly: `Folder "[trimmed folder name]" has been created.` |
| 5 | Create another folder using the exact name of an existing folder. | Creation is allowed; no duplicate-name error is shown. |
| 6 | Create another folder using a case variant of that existing folder name. | Creation is allowed; no duplicate-name error is shown. |

## Expected Final State

All temporary folders created during the trimming and duplicate-name checks exist (until cleanup removes them); the pre-existing duplicate-test folder is untouched; no folder was created from blank or whitespace-only input.

## Pass/Fail Criteria

**Pass:**
- Save is disabled/blocked for empty and whitespace-only input.
- A trimmed folder name is created and the toast reads exactly `Folder "[trimmed folder name]" has been created.`
- Creating a folder using an exact or case-variant duplicate name succeeds without a duplicate-name error.
- The Folder Name input receives focus automatically on modal open.

**Fail:**
- Save is enabled for empty/whitespace-only input, or a folder is created from such input.
- The created folder name is not trimmed, or the toast text does not match exactly.
- Duplicate or case-variant names are blocked or show an error.
- The input is not focused automatically on open.

## Cleanup

Delete only the temporary folders created by this case. Do not delete the pre-existing duplicate-test folder.
