---
id: ELITEA-3902
title: "Custom icon displayed in skills list page cardlist view"
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
- At least one Skill with custom icon exists
- At least one Skill without custom icon exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Skills page via sidebar | Skills page loads |
| 2 | Verify the page displays Skills in a card list view | Card list view is shown |
| 3 | Locate a Skill with a custom icon | Skill card is visible |
| 4 | Verify the card displays the custom icon, not the default SVG | Custom icon shown on card |
| 5 | Locate a Skill without a custom icon | Skill card is visible |
| 6 | Verify that Skill's card displays the default `skill-icon.svg` | Default SVG icon shown |

## Expected Final State

The Skills list page (CardList view) displays custom icons for Skills that have them and default icons for Skills without.

## Pass/Fail Criteria

**Pass:**
- Custom icon displays on card for Skill with custom icon
- Default SVG displays on card for Skill without custom icon

**Fail:**
- All cards show same icon
- Icons missing from cards
- Broken image icons displayed
