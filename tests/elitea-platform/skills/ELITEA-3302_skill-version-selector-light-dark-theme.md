---
id: ELITEA-3302
title: "Skills version selector displays correctly in light and dark themes"
priority: medium
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:skills, feat:version-selector, feat:theme, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor or Admin role
- Skill with multiple versions exists
- User can switch between light and dark themes

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Test Skill | Skill with multiple versions, including default version |

## Light Theme Validation

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Ensure light theme is active | Light theme applied to interface |
| 2 | Navigate to a Skill | Skill loads in light theme |
| 3 | Open version selector dropdown | Dropdown opens |
| 4 | Verify all text is visible and readable | Text has sufficient contrast |
| 5 | Verify icons (checkmark, pin) are visible | Icons visible with good contrast |
| 6 | Verify dropdown background and borders are visible | Dropdown has clear visual boundaries |
| 7 | Verify selected version highlight is visible | Selection indicator clearly visible |

## Dark Theme Validation

| # | Action | Expected Result |
|---|--------|-----------------|
| 8 | Switch to dark theme | Dark theme applied |
| 9 | Navigate to a Skill (or stay on current) | Skill displays in dark theme |
| 10 | Open version selector dropdown | Dropdown opens |
| 11 | Verify all text is visible and readable in dark theme | Text has sufficient contrast against dark background |
| 12 | Verify icons (checkmark, pin) are visible in dark theme | Icons visible with appropriate colors for dark theme |
| 13 | Verify dropdown background and borders are visible | Dropdown boundaries clear in dark theme |
| 14 | Verify selected version highlight is visible and distinct | Selection indicator visible with proper contrast |
| 15 | Verify pin icon for default version is visible | Pin icon stands out in dark theme |

## Theme Switching

| # | Action | Expected Result |
|---|--------|-----------------|
| 16 | With dropdown open, switch from light to dark theme | Dropdown updates theme correctly |
| 17 | Switch back to light theme | Dropdown updates to light theme |
| 18 | Verify no visual glitches during theme transition | Smooth transition, no broken styling |

## Expected Final State

Version selector dropdown is fully visible and readable in both light and dark themes. All elements (text, icons, backgrounds, highlights) have sufficient contrast and are appropriately styled for each theme.

## Pass/Fail Criteria

**Pass:**
- All text readable in both themes
- Icons visible with good contrast in both themes
- Dropdown backgrounds and borders clear in both themes
- Selected version highlight visible in both themes
- Pin icon visible in both themes
- Theme switching works smoothly
- No visual glitches or broken styling

**Fail:**
- Text not readable in one or both themes
- Icons invisible or low contrast
- Dropdown boundaries unclear
- Selection highlight not visible
- Pin icon not visible in dark theme
- Theme switching causes visual issues
- Contrast insufficient in either theme
