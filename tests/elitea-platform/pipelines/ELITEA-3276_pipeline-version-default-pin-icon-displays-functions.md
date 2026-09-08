---
id: ELITEA-3276
title: "Pipeline version default pin icon displays and functions correctly"
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
- Pipeline exists with a default version set (if default version functionality exists for Pipelines)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| Pipeline | Pipeline with default version configured |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to a Pipeline with a default version set | Pipeline loads |
| 2 | Open the version selector dropdown | Dropdown displays all versions |
| 3 | Locate the default version in the list | Default version is visible |
| 4 | Verify an active/filled pin icon is displayed next to the default version | Pin icon is visible and styled as active |
| 5 | Hover over the pin icon | Cursor changes to indicate interactivity |
| 6 | Verify tooltip displays "Default version" | Tooltip appears with correct text |
| 7 | Select a different version (not the default) | Non-default version loads |
| 8 | Open the version selector dropdown | Dropdown opens |
| 9 | Verify default version still shows pin icon | Pin icon remains on default version |
| 10 | Verify selected version shows checkmark (independent of pin) | Checkmark appears on selected version |
| 11 | Verify a version can be both default and selected | Both indicators can coexist |

## Expected Final State

Default version displays a pin icon with "Default version" tooltip. Pin indicator is independent of selected version indicator.

## Pass/Fail Criteria

**Pass:**
- Pin icon is visible on default version
- Tooltip displays "Default version" on hover
- Pin indicator is independent of selection indicator
- A version can show both pin and checkmark when it's default and selected

**Fail:**
- Pin icon is missing from default version
- Tooltip is missing or incorrect
- Pin indicator conflicts with selection indicator
- UI breaks when version is both default and selected

**Note:** If default version functionality does not exist for Pipelines, mark test as "Not Applicable" with note explaining Pipelines do not support default version feature.
