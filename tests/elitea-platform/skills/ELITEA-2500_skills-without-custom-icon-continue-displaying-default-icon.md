---
id: ELITEA-2500
title: "Skills without custom icon continue displaying default icon no visual regression"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5699]
---

## Preconditions

- User is logged in to `{{base_url}}`
- At least one Skill exists that has never had a custom icon set
- The Skill is attached to an Agent

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Skill | Skill without custom icon |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Identify a Skill that has never had a custom icon set | Skill identified |
| 2 | Navigate to Skills list page (CardList) | Page loads |
| 3 | Verify the Skill displays default `skill-icon.svg` | Default icon shown |
| 4 | Open the Skill detail/edit page | Page loads |
| 5 | Verify the Skill displays default `skill-icon.svg` | Default icon shown |
| 6 | Navigate to Agent configuration with this Skill attached | Agent edit page loads |
| 7 | Verify the SkillCard displays default `skill-icon.svg` | Default icon shown |
| 8 | Open SkillMenu dropdown (skill picker) | Dropdown opens |
| 9 | Verify the Skill displays default `skill-icon.svg` in dropdown | Default icon shown |
| 10 | Open Chat with Agent that has this Skill attached | Chat opens |
| 11 | Type `~` to trigger mention autocomplete | Autocomplete appears |
| 12 | Verify the Skill displays default `skill-icon.svg` | Default icon shown |
| 13 | Confirm no broken image icons, placeholder errors, or blank spaces appear in any location | All icons render correctly |

## Expected Final State

Existing Skills without a custom icon continue to display the default `skill-icon.svg` in all UI locations with no visual regression.

## Pass/Fail Criteria

**Pass:**
- Default icon displays in all 5 UI locations
- No broken images or blank spaces
- Consistent appearance across all locations

**Fail:**
- Broken image icon displayed
- Blank space instead of icon
- Inconsistent icons across locations
