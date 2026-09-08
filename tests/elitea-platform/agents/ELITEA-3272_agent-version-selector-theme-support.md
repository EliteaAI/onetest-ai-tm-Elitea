---
id: ELITEA-3272
title: "Agent — Version Selector Theme Support"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:version-selector, nfr:ui-themes, feat:agents, issue:6302]
requirements: [EliteaAI/elitea_issues#6302]
---
# ELITEA-3272: Agent — Version Selector Theme Support

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the version selector dropdown is visually correct and readable in both light and dark themes.

## Preconditions

- User logged in to ELITEA ({{base_url}})
- Agent exists with multiple versions
- User has access to theme switcher (light/dark mode)

## Test Data

| Field | Value |
|-------|-------|
| Test Agent | Agent with ≥3 versions |
| Themes to Test | Light theme, Dark theme |

## Steps — Light Theme

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Ensure the application is in light theme mode | Light theme is active |
| 2 | Navigate to the Agent configuration page | Agent page loads in light theme |
| 3 | Open the version selector dropdown | Dropdown opens |
| 4 | Verify all text elements are readable (version names, timestamps, creator info) | All text is clearly visible with sufficient contrast against background |
| 5 | Verify icons (checkmark, pin) are visible and clear | Icons are visible with good contrast |
| 6 | Verify background colors and borders are appropriate | Dropdown background, row backgrounds, and borders are visible and well-defined |
| 7 | Verify selected version highlight is visible | Selected version row has clear visual highlighting |
| 8 | Verify search input field is clearly visible and usable | Search field has clear border and readable placeholder text |

## Steps — Dark Theme

| # | Action | Expected Result |
|---|--------|----------------|
| 9 | Switch to dark theme mode | Dark theme is active |
| 10 | Navigate to (or refresh) the Agent configuration page | Agent page loads in dark theme |
| 11 | Open the version selector dropdown | Dropdown opens |
| 12 | Verify all text elements are readable | All text is clearly visible with sufficient contrast against dark background |
| 13 | Verify icons (checkmark, pin) are visible and clear in dark theme | Icons are visible with good contrast on dark background |
| 14 | Verify background colors and borders are appropriate for dark theme | Dropdown background, row backgrounds, and borders are visible and well-defined in dark mode |
| 15 | Verify selected version highlight is visible in dark theme | Selected version row has clear visual highlighting on dark background |
| 16 | Verify search input field is clearly visible in dark theme | Search field has clear border and readable placeholder text on dark background |
| 17 | Verify pin icon is visible in dark theme (if applicable) | Pin icon has sufficient contrast in dark theme |

## Expected Final State

Version selector dropdown is fully readable and visually correct in both light and dark themes; all elements have sufficient contrast and visibility.

## Pass/Fail Criteria

**Pass:** All text, icons, backgrounds, and borders are visible and readable in both light and dark themes; sufficient contrast maintained; no visual issues

**Fail:** Poor contrast in either theme; text or icons not visible; background/border issues; selected highlight not visible
