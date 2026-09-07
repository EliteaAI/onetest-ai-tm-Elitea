---
id: ELITEA-3207
title: "Regression: Create Folder auto-focus and keyboard behavior (#6485)"
priority: high
type: regression
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, issue:6485, regression, create-folder, keyboard]
requirements: [EliteaAI/elitea_issues#5194, EliteaAI/elitea_issues#6485]
---
# ELITEA-3207: Regression - Create Folder Auto-Focus and Keyboard Behavior

**Module:** Social Folders · **Priority:** High · **Type:** Regression

**Objective:** Re-verify, in a single consolidated pass, that Create Folder auto-focuses its input, blocks empty/whitespace-only submission, trims and shows the exact creation toast, and that Escape/Cancel/Enter behave correctly.

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
| 1 | Open Create Folder and type immediately without clicking the input. | The input is auto-focused and receives the text. |
| 2 | Attempt to save with empty and then whitespace-only input. | Save is blocked in both cases; no folder is created. |
| 3 | Enter a name with leading/trailing spaces and save. | The name is trimmed and the toast reads exactly: `Folder "[trimmed folder name]" has been created.` |
| 4 | Reopen, enter a name, and press Escape; then reopen, enter a name, and click Cancel. | Neither action creates a folder. |
| 5 | Reopen, enter a valid name, and press Enter with the input focused. | The folder is created exactly once. |

## Expected Final State

Only the folder created via the trimmed-name and Enter steps exists; no folder results from empty, whitespace, Escape, or Cancel attempts.

## Pass/Fail Criteria

**Pass:**
- The input auto-focuses on open.
- Empty/whitespace-only input blocks Save.
- The trimmed name is created with the exact toast copy.
- Escape and Cancel do not create a folder; Enter creates exactly one.

**Fail:**
- The input is not auto-focused.
- Empty/whitespace-only input is accepted.
- The toast text is incorrect or the name is not trimmed.
- Escape/Cancel create a folder, or Enter fails to submit or creates more than one.

## Cleanup

Delete any folders created during this case.
