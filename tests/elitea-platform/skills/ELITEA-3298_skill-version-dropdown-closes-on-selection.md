---
id: ELITEA-3298
title: "Skills version dropdown closes automatically after selecting version"
priority: medium
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
| 1 | Navigate to a Skill with multiple versions | Skill detail view loads |
| 2 | Open the version selector dropdown | Dropdown opens |
| 3 | Select a different version from the list | Version selection triggers |
| 4 | Verify the dropdown closes automatically | Dropdown closes |
| 5 | Verify the selected version is now displayed in the selector button/field | New version name displayed |
| 6 | Open the dropdown again | Dropdown opens |
| 7 | Select another version | Version selection triggers |
| 8 | Verify dropdown closes automatically again | Dropdown closes |

## Expected Final State

Version selector dropdown closes automatically after a version is selected, and the selected version is displayed in the selector component.

## Pass/Fail Criteria

**Pass:**
- Dropdown closes immediately after version selection
- Selected version name updates in selector display
- Behavior is consistent for all version selections
- No errors or UI glitches

**Fail:**
- Dropdown remains open after selection
- Selected version not displayed correctly
- Inconsistent close behavior
- Errors during selection process
