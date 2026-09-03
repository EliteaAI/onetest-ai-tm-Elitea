---
id: ELITEA-3202
title: "Rename a folder and preserve contents and open state"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, issue:6480, rename-folder]
requirements: [EliteaAI/elitea_issues#5194, EliteaAI/elitea_issues#6480]
---
# ELITEA-3202: Rename a Folder

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify that a folder can be renamed via the folder action menu with validation against whitespace-only input, an exact rename toast, and that the new name propagates everywhere while contents, count, and open state remain unchanged.

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
| 1 | Open a folder's action menu. | Rename and Delete are both available. |
| 2 | Select Rename. | Edit Folder opens pre-filled with the current name. |
| 3 | Clear the name and enter only whitespace. | Save is blocked. |
| 4 | Enter a unique new name and save. | The toast reads exactly: `Folder has been renamed to "[new folder name]".` |
| 5 | Inspect the folder everywhere it appears (panel, menus, open header if applicable). | The new name is shown everywhere; contents, count, and open state are unchanged. |

## Expected Final State

The folder has the new name everywhere it is displayed; its contents, count, and (if it was open) open state are unaffected by the rename.

## Pass/Fail Criteria

**Pass:**
- Rename and Delete are both available from the folder action menu.
- Whitespace-only input blocks Save.
- The rename toast reads exactly `Folder has been renamed to "[new folder name]".`
- The new name propagates everywhere; contents, count, and open state are unchanged.

**Fail:**
- Rename or Delete is missing from the action menu.
- Whitespace-only input is accepted.
- The toast text is missing or does not match exactly.
- The new name fails to propagate somewhere, or contents/count/open state change unexpectedly.

## Cleanup

Restore the folder's original name or delete it if temporary.
