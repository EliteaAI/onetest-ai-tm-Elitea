---
id: ELITEA-3203
title: "Delete a folder without deleting its entities"
priority: critical
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, issue:6480, delete-folder, confirmation]
requirements: [EliteaAI/elitea_issues#5194, EliteaAI/elitea_issues#6480]
---
# ELITEA-3203: Delete a Folder Without Deleting Its Entities

**Module:** Social Folders · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that deleting a folder shows an exact confirmation modal, that cancelling leaves everything unchanged, and that confirming deletes only the folder (with an exact toast) while its entities remain available and unfiled, including when the deleted folder was open.

## Entities to Test

Execute this case independently for each entity type below, using fresh disposable test data per entity. Do not share data or results between rows.

- [ ] Agents
- [ ] Skills
- [ ] Pipelines
- [ ] Toolkits & Indexes
- [ ] MCPs
- [ ] Credentials

## Preconditions

- A disposable folder contains at least two disposable/recoverable entities.
- Record the pin status of each entity before deletion.
- Execute the case once with the folder closed, and once with the folder open, where feasible.

## Steps

| # | Action | Expected Result |
|---|---|---|
| 1 | Open the folder action menu and select Delete. | The modal title reads exactly `Delete folder?` and the body reads exactly: `[Entity type] in this folder will not be deleted. They will be removed from the folder and remain available in the [Entity type] list.` |
| 2 | Click Cancel. | The modal closes; the folder and its entities are unchanged. |
| 3 | Reopen Delete and confirm. | The toast reads exactly: `Folder "[folder name]" has been deleted. Its items remain available in the [Entity type] list.` |
| 4 | Inspect the entities that were in the folder. | They remain available and unfiled; if the deleted folder was open, the complete unfiltered list is shown immediately. |
| 5 | Inspect pin status of the former entities. | Pin status is unchanged from the recorded baseline. |

## Expected Final State

The folder no longer exists; its former entities remain available, unfiled, and unmodified, including pin status; if the folder was open at deletion time, the view immediately shows the complete unfiltered list.

## Pass/Fail Criteria

**Pass:**
- The delete confirmation modal title and body match exactly the specified copy.
- Cancel leaves the folder and entities unchanged.
- Confirming shows the exact deletion toast and removes only the folder.
- Former entities remain available, unfiled, and with unchanged pin status.
- If the folder was open, the complete unfiltered list is shown immediately after deletion.

**Fail:**
- The modal title/body text is missing or does not match exactly.
- Cancel results in a change to the folder or its entities.
- Confirming deletes or otherwise alters any entity, or the toast text is wrong/missing.
- The view does not return to the complete list after deleting an open folder.

## Cleanup

No further cleanup is required; the folder is already deleted. Confirm entities remain intact and unfiled.
