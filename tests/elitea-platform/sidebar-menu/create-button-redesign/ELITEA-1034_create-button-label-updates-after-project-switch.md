---
id: ELITEA-1034
title: "Create Button Label Updates After Project Switch"
priority: high
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1034: Create Button Label Updates After Project Switch

**Module:** Create Button Redesign · **Priority:** High · **Type:** Functional

**Objective:** Verify that switching projects updates the Create button context to reflect the newly selected project scope.

**Coverage:**
- Project switch from Private to team project
- Create button state after switch
- Entity created belongs to the newly selected project

## Preconditions

- Logged in to ELITEA
- At least 2 projects available (Private + one team project)
- Sidebar in expanded state, on Agents section

## Test Data

At least 2 projects: Private + 1 team project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select "Private" project from the project switcher; navigate to Agents | Create button shows `+ Agent` scoped to Private project |
| 2 | Open the project switcher; select a team project | Project switches; all content updates to the team project |
| 3 | Observe the Create button label | Still shows `+ Agent` (same section, different project scope) |
| 4 | Click `+ Agent` | New Agent creation form opens in the context of the newly selected team project |
| 5 | Switch back to Private project while on Agents | Create button still shows `+ Agent`; clicking opens form in Private project context |

## Expected Final State

Create button still shows `+ Agent`; clicking opens form in Private project context

## Pass/Fail Criteria

**Pass:**
- Create button label remains correct after project switch
- Created entity belongs to the currently selected project

**Fail:**
- Create button label resets or shows wrong entity after project switch
- Entity is created in wrong project after switch
