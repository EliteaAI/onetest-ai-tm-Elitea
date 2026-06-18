---
id: ELITEA-1044
title: "Collapsed Sidebar Dropdown: Active Section Entity Has Checkmark"
priority: critical
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1044: Collapsed Sidebar Dropdown: Active Section Entity Has Checkmark

**Module:** Create Button Redesign · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that in the collapsed sidebar dropdown, the entity type corresponding to the current active section is visually indicated with a checkmark.

**Coverage:**
- Checkmark state for Agents, Pipelines, Chat, Credentials sections

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Sidebar in collapsed state

## Test Data

N/A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents (in expanded mode); then collapse sidebar | Agents section is active |
| 2 | Click `+` to open the collapsed dropdown | Dropdown opens; `Agent` item has a checkmark indicator |
| 3 | Close dropdown; navigate to Pipelines; reopen dropdown | `Pipeline` item has the checkmark; `Agent` does not |
| 4 | Close dropdown; navigate to Chat; reopen dropdown | `Conversation` item has the checkmark |
| 5 | Close dropdown; navigate to Credentials; reopen dropdown | `Credential` item has the checkmark |

## Expected Final State

`Credential` item has the checkmark

## Pass/Fail Criteria

**Pass:**
- Checkmark correctly reflects the active section's entity type on each navigation

**Fail:**
- No checkmark visible in dropdown
- Checkmark stays on wrong item after navigation
- Multiple items have checkmark simultaneously
