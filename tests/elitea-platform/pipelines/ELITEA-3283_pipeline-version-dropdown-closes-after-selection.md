---
id: ELITEA-3283
title: "Pipeline version dropdown closes automatically after version selection"
priority: medium
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
| 1 | Navigate to a Pipeline | Pipeline loads with current version |
| 2 | Open the version selector dropdown | Dropdown opens displaying all versions |
| 3 | Click on a different version in the list (e.g., "v1-production") | Version is selected |
| 4 | Verify the dropdown closes automatically | Dropdown is no longer visible |
| 5 | Verify the selected version name is now displayed in the selector button/field | Selector displays "v1-production" |
| 6 | Verify the Pipeline canvas updated to the selected version | Canvas reflects v1-production topology |
| 7 | Open the version selector dropdown again | Dropdown opens |
| 8 | Select the original version (e.g., "base") | Version is selected |
| 9 | Verify the dropdown closes automatically again | Dropdown closes |
| 10 | Verify the selector now displays "base" | Selector shows "base" |

## Expected Final State

After selecting a version from the dropdown, the dropdown closes automatically and the selector displays the newly selected version.

## Pass/Fail Criteria

**Pass:**
- Dropdown closes immediately after version selection
- Selected version name appears in the selector button/field
- Pipeline canvas updates to match selected version
- Behavior is consistent for all version selections
- No manual action required to close the dropdown

**Fail:**
- Dropdown remains open after version selection
- User must manually close the dropdown
- Selected version name doesn't appear in selector
- Dropdown closes before version loads
- Behavior is inconsistent
