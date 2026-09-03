---
id: ELITEA-3194
title: "Create Folder keyboard behavior: Escape, Cancel, and Enter"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, create-folder, keyboard]
requirements: [EliteaAI/elitea_issues#5194]
---
# ELITEA-3194: Create Folder Keyboard Behavior

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify that Escape and Cancel close the Create Folder modal without creating a folder, and that Enter (with the input focused) submits the form as Save, creating exactly one folder.

## Entities to Test

Execute this case independently for each entity type below, using fresh disposable test data per entity. Do not share data or results between rows.

- [ ] Agents
- [ ] Skills
- [ ] Pipelines
- [ ] Toolkits & Indexes
- [ ] MCPs
- [ ] Credentials

## Steps

| # | Action | Expected Result |
|---|---|---|
| 1 | Open Create Folder, enter a unique name, and press Escape. | The modal closes and the folder does not exist. |
| 2 | Reopen the modal, enter a different unique name, and click Cancel. | The modal closes and the folder does not exist. |
| 3 | Reopen the modal, enter a valid unique name, and press Enter while the input is focused. | The form submits as Save; the folder is created exactly once. |

## Expected Final State

No folder exists from the Escape or Cancel attempts; exactly one folder exists from the Enter submission (until cleanup removes it).

## Pass/Fail Criteria

**Pass:**
- Escape closes the modal without creating a folder.
- Cancel closes the modal without creating a folder.
- Enter (with input focused) submits the form as Save and creates exactly one folder.

**Fail:**
- Escape or Cancel results in a folder being created.
- Enter does not submit the form, or creates more than one folder.

## Cleanup

Delete any folder created by the Enter scenario.
