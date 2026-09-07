---
id: ELITEA-3192
title: "Folder panel baseline and empty state in Card and Table view"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, folder-panel, empty-state]
requirements: [EliteaAI/elitea_issues#5194]
---
# ELITEA-3192: Folder Panel Baseline and Empty State

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify that each supported entity listing page displays the FOLDERS section above TAGS in Card and Table view when no folders exist for the selected project and entity type.

## Entities to Test

Execute this case independently for each entity type below, using fresh disposable test data per entity. Do not share data or results between rows.

- [ ] Agents
- [ ] Skills
- [ ] Pipelines
- [ ] Toolkits & Indexes
- [ ] MCPs
- [ ] Credentials

## Preconditions

- The selected project and the entity type under test have no folders.
- The listing page supports the view being tested.

## Steps

| # | Action | Expected Result |
|---|---|---|
| 1 | Open the listing page for the selected entity type in Card view. | FOLDERS is visible above TAGS. |
| 2 | Inspect the Folders header and create control. | A create-folder `+` action is available and has an accessible name/tooltip of `Create folder`. |
| 3 | Inspect the empty panel. | `No folders created yet.` is displayed. |
| 4 | Switch to Table view. | FOLDERS remains above TAGS, with the same empty state and create action. |

## Expected Final State

FOLDERS is displayed above TAGS in both Card and Table view for the tested entity type, showing the empty state `No folders created yet.` and an accessible `Create folder` action, with no folders created.

## Pass/Fail Criteria

**Pass:**
- FOLDERS is displayed above TAGS in both Card and Table view.
- The create-folder `+` control is present with accessible name/tooltip `Create folder`.
- The empty panel displays exactly `No folders created yet.`

**Fail:**
- FOLDERS is missing, positioned incorrectly relative to TAGS, or absent in either view.
- The create-folder control is missing or lacks the `Create folder` accessible name/tooltip.
- The empty-state text is missing or does not read `No folders created yet.`

## Cleanup

Pass only when every selected entity-type row in the execution matrix passes all assertions.
