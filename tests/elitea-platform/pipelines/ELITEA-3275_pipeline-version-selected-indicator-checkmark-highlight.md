---
id: ELITEA-3275
title: "Pipeline version selected indicator displays checkmark and row highlight correctly"
priority: critical
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:pipelines, feat:version-selector, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor/Admin role
- Private project context is selected
- Pipeline exists with at least 2 versions

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| Pipeline | Pipeline with versions: "base", "v1-production" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to a Pipeline with multiple versions | Pipeline loads with currently selected version |
| 2 | Open the version selector dropdown | Dropdown displays list of versions |
| 3 | Locate the currently selected version row | Selected version is identifiable |
| 4 | Verify checkmark icon is displayed on the selected version | Checkmark icon is visible |
| 5 | Verify row highlight (background color/border) on selected version | Row has visual highlighting |
| 6 | Select a different version from the dropdown | New version loads |
| 7 | Open the version selector dropdown again | Dropdown opens |
| 8 | Verify the newly selected version shows checkmark and highlight | New version has checkmark and highlight |
| 9 | Verify the previous version no longer shows checkmark or highlight | Previous version has no indicators |

## Expected Final State

Only the currently selected version displays both a checkmark icon and row highlight. Previous selection indicators are removed.

## Pass/Fail Criteria

**Pass:**
- Selected version clearly shows checkmark icon
- Selected version row has visual highlighting
- Only one version shows selection indicators at a time
- Indicators update correctly when version changes

**Fail:**
- Checkmark or highlight missing from selected version
- Multiple versions show selection indicators
- Indicators don't update after version change
- Visual indicators are unclear or broken
