---
id: ELITEA-3200
title: "Open and close an empty folder and return to the complete list"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, issue:6483, empty-folder, folder-navigation]
requirements: [EliteaAI/elitea_issues#5194, EliteaAI/elitea_issues#6483]
---
# ELITEA-3200: Open and Close an Empty Folder

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify that opening an empty folder shows the exact empty-content message and a count of zero, and that closing or deselecting the folder restores the complete unfiltered list without redirecting to an entity creation page.

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
| 1 | Open a folder that contains no entities. | The panel displays exactly `No items in this folder yet.` and the count shows `(0)`. |
| 2 | Close or deselect the folder. | The complete unfiltered list is shown; there is no redirect to an entity Create page. |

## Expected Final State

The empty folder remains empty; the listing returns to the complete unfiltered view after closing.

## Pass/Fail Criteria

**Pass:**
- The empty-folder panel reads exactly `No items in this folder yet.` with a count of `(0)`.
- Closing/deselecting the folder shows the complete unfiltered list with no redirect.

**Fail:**
- The empty-state text is missing, incorrect, or the count is not `(0)`.
- Closing the folder redirects to a Create page or fails to restore the complete list.

## Cleanup

No data cleanup is required.
