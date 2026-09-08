---
id: ELITEA-3290
title: "Selected version indicator displays correctly in Skills version dropdown"
priority: critical
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:skills, feat:version-selector, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor or Admin role
- Skill with multiple versions exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Test Skill | Skill with at least 3 versions |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to a Skill with multiple versions | Skill detail view loads with current version displayed |
| 2 | Open the version selector dropdown | Dropdown opens |
| 3 | Locate the currently selected version in the list | Selected version row is visible |
| 4 | Verify checkmark icon is displayed next to selected version | Checkmark icon visible |
| 5 | Verify selected version row has visual highlighting (background color/border) | Row has distinct highlight styling |
| 6 | Select a different version from the dropdown | Version switches, dropdown closes or updates |
| 7 | Reopen the version selector dropdown | Dropdown opens again |
| 8 | Verify the newly selected version now shows checkmark and highlight | New version has checkmark and highlight |
| 9 | Verify the previous version no longer shows checkmark or highlight | Previous version styling returned to normal |

## Expected Final State

Currently selected version is clearly indicated with both a checkmark icon and row highlight. Indicators update correctly when version selection changes.

## Pass/Fail Criteria

**Pass:**
- Checkmark icon visible on selected version
- Selected version row has visual highlight (background/border)
- Only one version shows selection indicators at a time
- Indicators update immediately when selection changes

**Fail:**
- Checkmark missing or displayed on wrong version
- No row highlight on selected version
- Multiple versions show selection indicators
- Indicators don't update after version switch
