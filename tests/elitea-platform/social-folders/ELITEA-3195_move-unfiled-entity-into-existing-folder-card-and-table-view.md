---
id: ELITEA-3195
title: "Move an unfiled entity into an existing folder from Card and Table view"
priority: critical
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, issue:6480, move-entity, card-view]
requirements: [EliteaAI/elitea_issues#5194, EliteaAI/elitea_issues#6480]
---
# ELITEA-3195: Move an Unfiled Entity into an Existing Folder

**Module:** Social Folders · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an unfiled entity can be moved into an existing folder from both Card and Table view via Move to folder, with an exact toast, correct folder-count increment, exactly-once assignment, and no change to the entity's configuration, tags, permissions, versions, or pin state.

## Entities to Test

Execute this case independently for each entity type below, using fresh disposable test data per entity. Do not share data or results between rows.

- [ ] Agents
- [ ] Skills
- [ ] Pipelines
- [ ] Toolkits & Indexes
- [ ] MCPs
- [ ] Credentials

## Preconditions

- An existing folder contains no entities and has a recorded baseline count.
- Two unfiled entities are available: one for Card view and one for Table view.
- Record each entity's configuration, tags, permissions, versions, and pin state before moving.

## Steps

| # | Action | Expected Result |
|---|---|---|
| 1 | From Card view, open the action menu for an unfiled entity. | A folder icon is shown for the unfiled entity; hovering it shows the Move to folder action. |
| 2 | Move the unfiled entity to the existing folder. | The toast reads exactly: `"[entity name]" has been moved to "[folder name]".` |
| 3 | Inspect the target folder without refreshing. | Count increases by one and the entity is assigned exactly once. |
| 4 | Inspect the complete unfiltered list and entity data. | Entity remains available; configuration, tags, permissions, versions, and pin state are unchanged. |
| 5 | In Table view, open the Actions menu for a second unfiled entity. | Move to folder is available; Create folder is at the top and Remove from folder is at the bottom of the folder menu when applicable. |
| 6 | Move the second unfiled entity to the same folder. | The toast reads exactly: `"[entity name]" has been moved to "[folder name]".` The count increases by one again and the entity data remains unchanged. |

## Expected Final State

Both entities (Card-view and Table-view) are assigned to the target folder exactly once each; the folder count reflects both moves; entity configuration, tags, permissions, versions, and pin state are unchanged.

## Pass/Fail Criteria

**Pass:**
- Toast reads exactly `"[entity name]" has been moved to "[folder name]".` for both moves.
- Folder count increases by one per move, with each entity assigned exactly once.
- Entity configuration, tags, permissions, versions, and pin state remain unchanged after the move.
- Create folder appears at the top and Remove from folder at the bottom of the folder menu when applicable.

**Fail:**
- The toast text differs from the exact copy, is missing, or is duplicated.
- The folder count does not increase, drifts, or an entity is assigned more than once.
- Entity configuration, tags, permissions, versions, or pin state change as a result of the move.

## Cleanup

Remove both temporary assignments from the folder and verify the count returns to its recorded baseline.
