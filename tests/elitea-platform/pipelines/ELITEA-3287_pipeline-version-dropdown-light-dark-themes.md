---
id: ELITEA-3287
title: "Pipeline version dropdown displays correctly in light and dark themes"
priority: medium
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:pipelines, feat:version-selector, feat:themes, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor/Admin role
- Private project context is selected
- Pipeline exists with multiple versions
- User has access to theme settings

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| Pipeline | Pipeline with multiple versions (base, published, draft) |

## Steps: Light Theme

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Ensure light theme is active | Application displays in light theme |
| 2 | Navigate to a Pipeline | Pipeline loads in light theme |
| 3 | Open the version selector dropdown | Dropdown opens |
| 4 | Verify all text is visible and readable (version names, timestamps, creators) | All text has sufficient contrast and is legible |
| 5 | Verify icons (checkmark, pin) are visible | Icons are clearly visible |
| 6 | Verify background colors and borders are appropriate | Colors match light theme aesthetics |
| 7 | Verify selected version highlight is visible | Row highlight is clear in light theme |
| 8 | Verify hover states are visible | Hover effects are noticeable |

## Steps: Dark Theme

| # | Action | Expected Result |
|---|--------|-----------------|
| 9 | Switch to dark theme (via Settings or theme toggle) | Application displays in dark theme |
| 10 | Navigate to the same Pipeline | Pipeline loads in dark theme |
| 11 | Open the version selector dropdown | Dropdown opens |
| 12 | Verify all text is visible and readable | All text has sufficient contrast for dark theme |
| 13 | Verify icons (checkmark, pin) are visible | Icons are clearly visible in dark theme |
| 14 | Verify background colors and borders match dark theme | Colors are appropriate for dark theme |
| 15 | Verify selected version highlight is visible | Row highlight has good contrast in dark theme |
| 16 | Verify hover states are visible | Hover effects are noticeable in dark theme |
| 17 | Verify search input field styling matches dark theme | Search field is styled appropriately |

## Steps: Theme Consistency

| # | Action | Expected Result |
|---|--------|-----------------|
| 18 | Compare dropdown visual quality in both themes | Both themes provide good readability and aesthetics |
| 19 | Verify no color contrast issues in either theme | WCAG contrast guidelines are met in both themes |

## Expected Final State

Version selector dropdown is fully functional and visually correct in both light and dark themes with sufficient contrast and readability.

## Pass/Fail Criteria

**Pass:**
- All text is readable in both themes (sufficient contrast)
- Icons are visible in both themes
- Background colors and borders match theme aesthetics
- Selected version highlight is clear in both themes
- Hover states are visible in both themes
- No visual artifacts or color issues
- WCAG contrast guidelines are met

**Fail:**
- Text is difficult to read in one or both themes
- Icons are invisible or hard to see
- Colors don't match theme or clash
- Selected version highlight is unclear
- Hover states are not visible
- Color contrast fails WCAG guidelines
- Visual artifacts or rendering issues occur
