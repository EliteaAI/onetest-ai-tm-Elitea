---
id: ELITEA-3297
title: "Skills version dropdown closes when clicking outside"
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
| Test Skill | Any Skill with multiple versions |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to a Skill | Skill detail view loads |
| 2 | Open the version selector dropdown | Dropdown opens |
| 3 | Click outside the dropdown area (e.g., page header) | Dropdown closes |
| 4 | Open the dropdown again | Dropdown opens |
| 5 | Click on the sidebar navigation | Dropdown closes |
| 6 | Open the dropdown again | Dropdown opens |
| 7 | Click on the main content area outside the dropdown | Dropdown closes |
| 8 | Open the dropdown again | Dropdown opens |
| 9 | Click on the page footer or any other area outside dropdown | Dropdown closes |

## Expected Final State

Version selector dropdown closes correctly when user clicks anywhere outside the dropdown area.

## Pass/Fail Criteria

**Pass:**
- Dropdown closes immediately when clicking outside
- Works for all clickable areas (header, sidebar, content, footer)
- Dropdown can be reopened after closing
- No errors or unexpected behavior

**Fail:**
- Dropdown remains open after outside click
- Dropdown doesn't close for certain areas
- Errors occur when clicking outside
- Dropdown cannot be reopened
