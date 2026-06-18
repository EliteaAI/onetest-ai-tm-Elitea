---
id: ELITEA-1018
title: "Icons for All Four Fixed Items Render Correctly in Both Themes [Parametrized]"
priority: medium
type: functional
module: sidebar-menu
status: ready
execution_type: manual
tags: [nfr:usability, r-2.0.1, 3846]
requirements: [ProjectAlita/projectalita.github.io#3846]
---
# ELITEA-1018: Icons for All Four Fixed Items Render Correctly in Both Themes [Parametrized]

**Module:** Sidebar Menu · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the outlined icons for Applications, Personalization, Analytics, and Environment are clearly visible and retain their outlined style in both Light and Dark modes.

**Coverage:**
- Applications icon visible in Light and Dark mode
- Personalization icon visible in Light and Dark mode
- Analytics icon visible in Light and Dark mode
- Environment icon visible in Light and Dark mode (Public project)

## Preconditions

- User is logged in with access to Private/Team and Public projects
- Browser: Chrome (latest)

## Test Data

| # | Icon | Theme | Project Type |
|---|---|---|---|
| 1 | Applications | Light | Private/Team |
| 2 | Applications | Dark | Private/Team |
| 3 | Personalization | Light | Private/Team |
| 4 | Personalization | Dark | Private/Team |
| 5 | Analytics | Light | Private/Team |
| 6 | Analytics | Dark | Private/Team |
| 7 | Environment | Light | Public |
| 8 | Environment | Dark | Public |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enable Light mode. Navigate to a Private/Team project and expand the sidebar. | Sidebar visible in Light mode. |
| 2 | Locate each of the following: Applications, Personalization, Analytics icons. | All three icons are clearly visible with proper contrast against the light sidebar background. |
| 3 | Switch to a Public project in Light mode. Locate the Environment icon. | Environment icon is clearly visible with proper contrast. |
| 4 | Switch to Dark mode. Navigate to a Private/Team project. | Sidebar visible in Dark mode. |
| 5 | Locate Applications, Personalization, Analytics icons in Dark mode. | All three icons are clearly visible with proper contrast against the dark sidebar background. |
| 6 | Switch to a Public project in Dark mode. Locate the Environment icon. | Environment icon is clearly visible in Dark mode. |
| 7 | In each case, confirm no icon appears as: invisible (white on white / black on black), filled instead of outlined, or a different incorrect icon. | All 4 icons consistently display outlined style with no contrast issues in either theme. |

## Expected Final State

All 4 icons consistently display outlined style with no contrast issues in either theme.

## Pass/Fail Criteria

**Pass:**
- All four icons are clearly visible in both Light and Dark modes
- All icons retain outlined style (not filled) in both themes
- No contrast issues (white-on-white, dark-on-dark)

**Fail:**
- Any icon invisible or extremely low contrast in either theme
- Any icon reverts to filled style in either theme
- Wrong icon displayed for any menu item
