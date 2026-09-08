---
id: ELITEA-3299
title: "Keyboard navigation works in Skills version selector"
priority: medium
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:skills, feat:version-selector, feat:accessibility, eng:frontend, r-2.0.6]
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
| Test Skill | Skill with at least 4 versions |
| Keyboard keys | Arrow Down, Arrow Up, Enter, Escape |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to a Skill with multiple versions | Skill loads |
| 2 | Tab to the version selector component | Version selector receives focus (visible focus indicator) |
| 3 | Press Enter or Space key | Dropdown opens |
| 4 | Press Arrow Down key | Focus moves to next version in list |
| 5 | Press Arrow Down key again | Focus moves to next version |
| 6 | Press Arrow Up key | Focus moves to previous version |
| 7 | Press Enter key while a version is focused | Version is selected, dropdown closes |
| 8 | Open dropdown again | Dropdown opens |
| 9 | Press Escape key | Dropdown closes without changing selection |
| 10 | Open dropdown and tab to search field | Search field receives focus |
| 11 | Type search query | List filters as typing |
| 12 | Press Arrow Down from search field | Focus moves to first filtered result |
| 13 | Press Enter on highlighted version | Version selected, dropdown closes |

## Expected Final State

Version selector dropdown supports full keyboard navigation: arrow keys to navigate, Enter to select, Escape to close, Tab to move focus.

## Pass/Fail Criteria

**Pass:**
- Tab navigation focuses version selector
- Enter/Space opens dropdown
- Arrow keys navigate version list
- Enter selects focused version
- Escape closes dropdown
- Search field accepts keyboard input
- Focus indicators visible throughout
- All keyboard interactions work smoothly

**Fail:**
- Keyboard navigation doesn't work
- Arrow keys don't move focus
- Enter doesn't select version
- Escape doesn't close dropdown
- Focus indicators missing
- Keyboard trap in dropdown
