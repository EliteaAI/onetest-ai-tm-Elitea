---
id: ELITEA-3211
title: "Regression: Selecting a folder resets pagination to page 1 (#6423)"
priority: high
type: regression
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, issue:5194, issue:6423, regression, pagination]
requirements: [EliteaAI/elitea_issues#5194, EliteaAI/elitea_issues#6423]
---
# ELITEA-3211: Regression - Folder Selection Resets Pagination

**Module:** Social Folders · **Priority:** High · **Type:** Regression

**Objective:** Re-verify that selecting a folder while viewing a page beyond page 1 resets pagination to page 1/offset 0 and shows the folder's entities without a false empty state.

## Entities to Test

Execute this case independently for each entity type below. Do not share data or results between rows.

- [ ] Agents
- [ ] Skills
- [ ] Pipelines
- [ ] Toolkits & Indexes
- [ ] MCPs
- [ ] Credentials

## Preconditions

- Enough entities exist in the unfiltered list to reach page 2 or beyond.
- A folder exists containing fewer entities than the current page offset.

## Steps

| # | Action | Expected Result |
|---|---|---|
| 1 | Navigate to page 2 or later of the unfiltered list. | The later page is displayed. |
| 2 | Select the prepared folder. | Pagination resets to page 1/offset 0; the folder's entities are shown; no false empty state appears. |

## Expected Final State

The folder's entities are shown starting from page 1, matching its actual contents.

## Pass/Fail Criteria

**Pass:** Selecting the folder resets pagination to page 1 and shows its entities correctly with no false empty state.

**Fail:** Pagination remains on the prior offset, causing a false empty state or incorrect/missing entities.

## Cleanup

No data cleanup is required beyond any disposable folder created for setup.
