---
id: ELITEA-4066
title: "Project theme applies admin-configured custom colors immediately without page reload"
priority: high
type: functional
module: settings/preferences
status: ready
execution_type: manual
tags: [feat:settings, feat:custom-theme, live-preview]
requirements: []
---

# ELITEA-4066: Project theme applies admin-configured custom colors immediately without page reload

**Module:** settings/preferences · **Priority:** high · **Type:** functional

**Objective:** Verify that selecting "Project" theme in user preferences applies the admin-configured custom colors immediately without requiring a page reload (live preview functionality).

---

## Preconditions

- Admin has configured custom theme colors in Admin Portal (Features → Custom Theme)
- Custom theme has been saved with distinctive colors (e.g., Primary Main: #3FD99B)
- User is logged into ELITEA platform with any role
- User is currently on a theme other than "Project" (Dark or Light)

---

## Test Data

| Field | Value |
|-------|-------|
| Admin configured Primary Main | #3FD99B (or other distinctive color) |
| Test page | Settings > Preferences |

---

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Note the current UI colors (sidebar background, button colors, accent colors) | Current theme colors are observed and documented |
| 2 | Navigate to Settings > Preferences | Preferences page loads with GENERAL section visible |
| 3 | Locate the Theme selector showing options: System, Dark, Light, Project | All four theme options are displayed as selectable cards/buttons |
| 4 | Click on "Project" theme option | Theme selection registers immediately |
| 5 | Observe UI colors immediately after selection (do not refresh) | UI colors change to admin-configured custom theme colors instantly |
| 6 | Verify sidebar background reflects custom theme | Sidebar shows custom theme background color |
| 7 | Verify accent colors (buttons, links, icons) reflect custom theme | Primary accent colors match admin-configured Primary Main color |
| 8 | Navigate to another page (e.g., Agents, Prompts) without refreshing | Custom theme colors persist across navigation |

---

## Expected Final State

Custom theme colors are applied immediately upon selection without any page reload, and all UI components reflect the admin-configured color palette.

---

## Pass/Fail Criteria

**Pass:**
- Theme changes apply instantly without page reload
- All visible UI components reflect custom theme colors
- No flash of default theme during transition
- Colors persist when navigating between pages

**Fail:**
- Page reload is required to see theme changes
- Some UI components retain previous theme colors
- Colors do not match admin-configured values
- Visual glitches or flashing during theme transition
