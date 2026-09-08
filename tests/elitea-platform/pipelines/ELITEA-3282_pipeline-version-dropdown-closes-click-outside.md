---
id: ELITEA-3282
title: "Pipeline version dropdown closes correctly when clicking outside"
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
- Pipeline exists with multiple versions

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| Pipeline | Any Pipeline with at least 2 versions |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to a Pipeline | Pipeline loads |
| 2 | Open the version selector dropdown | Dropdown opens with version list |
| 3 | Click on the page header area (outside the dropdown) | Dropdown closes |
| 4 | Verify the dropdown is no longer visible | Dropdown is hidden |
| 5 | Open the version selector dropdown again | Dropdown opens |
| 6 | Click on the sidebar (outside the dropdown) | Dropdown closes |
| 7 | Open the dropdown again | Dropdown opens |
| 8 | Click on the main canvas/content area (outside the dropdown) | Dropdown closes |
| 9 | Open the dropdown again | Dropdown opens |
| 10 | Click on the Pipeline name/title area (outside the dropdown) | Dropdown closes |
| 11 | Verify dropdown behavior is consistent across all click-outside scenarios | Dropdown always closes when clicking outside |

## Expected Final State

Version selector dropdown closes reliably when user clicks anywhere outside the dropdown area.

## Pass/Fail Criteria

**Pass:**
- Dropdown closes when clicking page header
- Dropdown closes when clicking sidebar
- Dropdown closes when clicking main content area
- Dropdown closes when clicking any area outside the dropdown
- Behavior is consistent across all scenarios
- No errors occur

**Fail:**
- Dropdown remains open after clicking outside
- Dropdown behavior is inconsistent
- Some click-outside areas don't close the dropdown
- Errors occur during interaction
