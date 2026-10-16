---
id: ELITEA-3898
title: "Custom icon displayed in skillmenu dropdown skill picker"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5699]
---

## Preconditions

- User is logged in to `{{base_url}}` as Admin or Editor role
- At least one Skill with custom icon exists
- At least one Skill without custom icon exists (uses default)
- At least one Agent exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Skill A | Skill with custom icon |
| Skill B | Skill without custom icon (default) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents page | Agents page loads |
| 2 | Open an Agent's edit page | Agent edit form loads |
| 3 | Click **+ Skill** to open the SkillMenu dropdown | SkillMenu dropdown opens with list of available Skills |
| 4 | Locate Skill A (with custom icon) in the dropdown list | Skill A is visible |
| 5 | Verify the custom icon is displayed next to Skill A's name | Custom icon shown |
| 6 | Locate Skill B (without custom icon) in the dropdown list | Skill B is visible |
| 7 | Verify the default `skill-icon.svg` is displayed next to Skill B's name | Default SVG icon shown |

## Expected Final State

The SkillMenu dropdown displays custom icons for Skills that have them and default icons for Skills without custom icons.

## Pass/Fail Criteria

**Pass:**
- Custom icon shows for Skill with custom icon
- Default SVG shows for Skill without custom icon
- All Skills in dropdown have appropriate icons

**Fail:**
- All Skills show same icon regardless of custom setting
- Icons missing entirely
- Wrong icons displayed
