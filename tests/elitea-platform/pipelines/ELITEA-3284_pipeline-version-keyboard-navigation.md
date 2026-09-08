---
id: ELITEA-3284
title: "Pipeline version selector supports keyboard navigation"
priority: medium
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:pipelines, feat:version-selector, feat:accessibility, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor/Admin role
- Private project context is selected
- Pipeline exists with at least 3 versions

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| Pipeline | Pipeline with versions: "base", "v1", "v2", "v3" |

## Steps: Opening and Navigating with Keyboard

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to a Pipeline | Pipeline loads |
| 2 | Tab to the version selector component | Selector receives focus (visual focus indicator) |
| 3 | Press Enter or Space to open the dropdown | Dropdown opens |
| 4 | Press Down Arrow key | Focus moves to next version in the list |
| 5 | Press Down Arrow again | Focus moves to the next version |
| 6 | Press Up Arrow key | Focus moves back to previous version |
| 7 | Press Home key (if supported) | Focus moves to first version in list |
| 8 | Press End key (if supported) | Focus moves to last version in list |

## Steps: Search and Selection

| # | Action | Expected Result |
|---|--------|-----------------|
| 9 | Type characters (e.g., "v") | Search field receives input and filters list |
| 10 | Press Down Arrow | Focus moves through filtered results |
| 11 | Press Enter on a focused version | Version is selected, dropdown closes, canvas updates |
| 12 | Tab to version selector and press Enter to open dropdown | Dropdown opens |
| 13 | Press Escape key | Dropdown closes without changing selection |

## Expected Final State

Version selector dropdown fully supports keyboard navigation including arrow keys for focus movement, Enter/Space for opening and selection, and Escape for closing.

## Pass/Fail Criteria

**Pass:**
- Version selector is keyboard accessible (can be focused via Tab)
- Enter/Space opens the dropdown
- Arrow keys navigate through versions
- Enter selects a focused version
- Escape closes the dropdown
- Visual focus indicators are clear
- Keyboard navigation works with search filtering
- All interactions are smooth and intuitive

**Fail:**
- Version selector cannot be accessed via keyboard
- Arrow keys don't navigate versions
- Enter doesn't select or open
- Escape doesn't close dropdown
- No visual focus indicators
- Keyboard navigation is broken or inconsistent
