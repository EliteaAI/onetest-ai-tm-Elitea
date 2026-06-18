---
id: ELITEA-0676
title: "Fork Wizard Opens in Fork Mode with Source Project Excluded from Target Dropdown"
priority: critical
type: functional
module: fork
status: ready
execution_type: manual
tags: [feat:import-forking, story:3728, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3728]
---
# ELITEA-0676: Fork Wizard Opens in Fork Mode with Source Project Excluded from Target Dropdown

**Module:** Fork · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking Fork opens the Import Wizard in fork mode (correct title, Fork button) and that the source project is excluded from the target project dropdown.

**Coverage:**
- Wizard mode differentiation (fork vs import)
- Target project dropdown population and filtering
- Source project exclusion from selectable targets

## Preconditions

- Logged in as Editor in Source Project
- At least two other accessible projects exist

## Test Data

- Any agent in Source Project
- Source Project name noted for verification

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Source Project → Agents → click Fork on any agent | Fork wizard modal opens |
| 2 | Check the modal title | Title reads "Fork parameters" (not "Import parameters") |
| 3 | Click the Target Project dropdown | Dropdown opens and is populated with project names |
| 4 | Scan the dropdown list for the current Source Project | Source Project does not appear in the list |
| 5 | Select a valid Target Project | Fork button becomes active |
| 6 | Verify the action button label | Button reads "Fork" (not "Import") |

## Expected Final State

Button reads "Fork" (not "Import")

## Pass/Fail Criteria

**Pass:**
- Modal title is "Fork parameters"
- Source project is absent from the target dropdown
- Button label is "Fork"

**Fail:**
- Modal title says "Import parameters"
- Source project appears and is selectable as the target
- Button label is "Import"
