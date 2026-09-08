---
id: ELITEA-3292
title: "Version switching updates Skill interface correctly"
priority: critical
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:skills, feat:version-selector, eng:frontend, eng:backend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor or Admin role
- Skill with at least 2 versions exists, with different instructions in each version

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Test Skill | Skill with versions containing different instruction content |
| Version 1 | "Calculate the sum of two numbers" |
| Version 2 | "Calculate the product of two numbers" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to a Skill with multiple versions | Skill detail view loads |
| 2 | Note the current version displayed in the selector | Current version name visible |
| 3 | Note the skill instructions displayed | Instructions from current version visible |
| 4 | Open the version dropdown and select a different version | Version selection triggers |
| 5 | Verify the version selector now displays the newly selected version name | Selector updates to show new version |
| 6 | Verify the skill instructions update to show the selected version's content | Instructions change to match selected version |
| 7 | Verify any attached resources (if applicable) update to the selected version | Resources update correctly |
| 8 | Switch back to the original version | Original version selected |
| 9 | Verify instructions revert to original version content | Instructions match original version |

## Expected Final State

Selecting a different version updates the version selector display and loads the selected version's skill instructions and configuration.

## Pass/Fail Criteria

**Pass:**
- Version selector display updates to new version name
- Skill instructions update to match selected version
- All configuration updates correctly
- Switching is smooth without errors

**Fail:**
- Version selector doesn't update display
- Instructions remain unchanged after switch
- Configuration doesn't load for new version
- Errors occur during version switch
