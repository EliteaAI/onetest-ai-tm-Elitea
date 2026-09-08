---
id: ELITEA-3296
title: "Version selector UI is visually consistent in Skills"
priority: high
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
- Skills with version selectors exist

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Reference | Compare against Agents and Pipelines version selectors |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open version selector dropdown in a Skill | Dropdown opens |
| 2 | Note styling: dropdown width, row height, font sizes, icon sizes, spacing | Visual characteristics observed |
| 3 | Navigate to Agents section and open a version selector | Agent version dropdown opens |
| 4 | Compare styling to Skills version selector | Styling matches (width, height, fonts, icons, spacing) |
| 5 | Navigate to Pipelines section and open a version selector | Pipeline version dropdown opens |
| 6 | Compare styling to Skills and Agents version selectors | All three match in styling |
| 7 | In Skills dropdown, verify search input field styling | Search field styling consistent |
| 8 | Verify metadata display layout (timestamp, creator) is consistent | Layout matches across components |
| 9 | Verify icon positioning (checkmark, pin) is consistent | Icons positioned consistently |
| 10 | Check dropdown border, shadow, and background styling | Visual effects consistent |

## Expected Final State

Version selector dropdown has consistent styling, layout, and behavior across Skills, matching the implementation in Agents and Pipelines.

## Pass/Fail Criteria

**Pass:**
- Dropdown width, height, and dimensions match across components
- Font sizes and weights consistent
- Icon sizes and positioning consistent
- Spacing and padding consistent
- Search field styling matches
- Metadata layout consistent
- Overall visual appearance unified

**Fail:**
- Visual inconsistencies between Skills and other components
- Different dimensions or spacing
- Icon positioning varies
- Font or color differences
- Layout discrepancies
