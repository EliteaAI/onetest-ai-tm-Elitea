---
id: ELITEA-3430
title: "Participant Picker Search Finds and Selects Any Agent or Pipeline in the Project"
priority: low
type: functional
module: chat
status: draft
execution_type: manual
tags: [feat:chat, feat:project-setup, story:6358, default-chat-config, search]
requirements: [EliteaAI/elitea_issues#6358]
---
# ELITEA-3430: Participant Picker Search Finds and Selects Any Agent or Pipeline in the Project

**Module:** Chat · **Priority:** Low · **Type:** Functional

**Objective:** Confirm the search box in the "Pre-configured participants" picker correctly filters and allows selecting any agent or pipeline in the project, not just ones visible without scrolling.

**Coverage:** Usability — the picker must scale to projects with many agents/pipelines.

## Preconditions

- The project has enough agents and pipelines that not all fit on screen without scrolling (10+ combined, spread across different name prefixes)
- Logged in as a project admin

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the "Pre-configured participants" picker. | List of available agents/pipelines is shown. |
| 2 | Type a partial name matching an agent near the start of the alphabetical/default list. | Search filters to matching results; the agent is selectable. |
| 3 | Clear the search and type a partial name matching an agent or pipeline near the end of the list (one that would require scrolling without search). | Search still finds and surfaces it correctly. |
| 4 | Select the item found in step 3 and Save. | It is added successfully to the preconfigured list. |
| 5 | Repeat steps 2–4 for a pipeline (not just agents). | Pipelines are equally searchable and selectable. |

## Expected Final State

Every agent and pipeline in the project is findable via search in the picker and can be added as a preconfigured participant, regardless of its position in the underlying list.

## Pass/Fail Criteria

**Pass:**
- Steps 2, 3, and 5 all return correct, selectable matches

**Fail:**
- Search misses valid matches, returns stale/incorrect results, or an item found via search cannot actually be selected/saved
