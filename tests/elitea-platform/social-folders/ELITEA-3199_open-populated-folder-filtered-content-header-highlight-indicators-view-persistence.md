---
id: ELITEA-3199
title: "Open a populated folder and verify filtered content, header, highlight, indicators, and view persistence"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, folder-navigation, folder-indicator]
requirements: [EliteaAI/elitea_issues#5194]
---
# ELITEA-3199: Open a Populated Folder

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify that opening a populated folder filters the listing to only its entities, shows a correct header (icon, name, count, Close folder action) and panel highlight, preserves these across a Card/Table view switch, and that closing the folder restores the full unfiltered list while the folder indicator and tags remain visible on the entity.

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
| 1 | Open a folder containing at least two entities. | Only its entities are displayed. |
| 2 | Inspect the folder header. | Header shows folder icon, name, item count, and close action with accessible name/tooltip `Close folder`. |
| 3 | Inspect the Folders panel. | The selected folder is visibly highlighted. |
| 4 | Inspect a folder entity in the open view. | Folder indicator shows the folder association without replacing existing tags. |
| 5 | Switch Card to Table and back. | Folder, filtered contents, header, and highlight remain correct. |
| 6 | Close the folder and inspect the same entity in the full list. | Full unfiltered list is shown; folder indicator and tags remain present. |

## Expected Final State

After closing the folder, the full unfiltered list is shown again and the previously filed entity retains its folder indicator and tags; the Card/Table view selection persists throughout.

## Pass/Fail Criteria

**Pass:**
- Opening the folder shows only its entities, with a correct header (icon, name, count, `Close folder` action) and panel highlight.
- The folder indicator is shown on entities without replacing existing tags.
- Switching Card/Table and back preserves the folder, filtered contents, header, and highlight.
- Closing the folder restores the full unfiltered list while the folder indicator and tags remain visible on the entity.

**Fail:**
- The folder shows entities outside the folder, or the header/count/highlight is missing or incorrect.
- The folder indicator replaces or hides existing tags.
- Switching views loses the folder filter, header, or highlight.
- Closing the folder does not restore the full list, or the folder indicator/tags disappear afterward.

## Cleanup

No data cleanup is required.
