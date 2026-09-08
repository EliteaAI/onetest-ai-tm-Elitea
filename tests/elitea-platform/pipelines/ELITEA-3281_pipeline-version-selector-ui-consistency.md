---
id: ELITEA-3281
title: "Pipeline version selector UI consistency with other components"
priority: high
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
- Access to Agents, Pipelines, and Skills sections

## Test Data

| Field | Value |
|-------|-------|
| Agent URL | `{{base_url}}/app/agents` |
| Pipeline URL | `{{base_url}}/app/pipelines` |
| Skill URL | `{{base_url}}/app/skills` |

## Steps: Compare Styling Across Components

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agents and open a version selector dropdown | Dropdown opens |
| 2 | Note dropdown width, row height, font sizes, icon sizes, spacing | Record visual properties |
| 3 | Navigate to Pipelines and open a version selector dropdown | Dropdown opens |
| 4 | Compare dropdown width with Agents | Width matches Agents |
| 5 | Compare row height with Agents | Row height matches Agents |
| 6 | Compare font sizes with Agents | Font sizes match Agents |
| 7 | Compare icon sizes (checkmark, pin) with Agents | Icon sizes match Agents |
| 8 | Compare spacing and padding with Agents | Spacing matches Agents |
| 9 | Navigate to Skills and open a version selector dropdown | Dropdown opens |
| 10 | Compare Skills dropdown styling with Agents and Pipelines | Styling matches both components |

## Steps: Search Input Consistency

| # | Action | Expected Result |
|---|--------|-----------------|
| 11 | Compare search input field styling across all three components | Search field styling is identical |
| 12 | Verify placeholder text is consistent | Placeholder text matches across components |

## Steps: Metadata Display Consistency

| # | Action | Expected Result |
|---|--------|-----------------|
| 13 | Compare metadata display layout (version name, timestamp, creator) across components | Layout is consistent |
| 14 | Verify metadata text sizes and colors match | Text styling is uniform |

## Steps: Icon Positioning Consistency

| # | Action | Expected Result |
|---|--------|-----------------|
| 15 | Compare checkmark icon positioning across components | Checkmark position is consistent |
| 16 | Compare pin icon positioning across components | Pin icon position is consistent |

## Expected Final State

Version selector dropdown has identical styling, layout, and behavior across Agents, Pipelines, and Skills components.

## Pass/Fail Criteria

**Pass:**
- Dropdown dimensions (width, row height) are consistent across all components
- Font sizes and icon sizes match
- Spacing and padding are uniform
- Search input field styling is identical
- Metadata display layout is consistent
- Icon positioning is uniform
- Overall visual appearance is cohesive

**Fail:**
- Dropdown styling differs between components
- Inconsistent dimensions or spacing
- Font or icon sizes vary
- Search field styling is different
- Metadata layout varies
- Icon positioning is inconsistent
- Visual inconsistencies detract from user experience
