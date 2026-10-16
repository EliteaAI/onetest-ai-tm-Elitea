---
id: ELITEA-4073
title: "Selecting Dark mode applies standard dark theme correctly"
priority: high
type: functional
module: settings/preferences
status: ready
execution_type: manual
tags: [feat:settings, theme, dark-mode]
requirements: []
---

# ELITEA-4073: Selecting Dark mode applies standard dark theme correctly

**Module:** settings/preferences · **Priority:** high · **Type:** functional

**Objective:** Verify that selecting "Dark" theme option applies the standard dark color palette consistently across all UI components.

---

## Preconditions

- User is logged into ELITEA platform
- Current theme is set to Light or Project (not Dark)
- User has access to Settings > Preferences

---

## Test Data

| Field | Value |
|-------|-------|
| Expected background | Dark (#1a1a2e or similar dark shade) |
| Expected text | Light colors for contrast |
| Test pages | Agents, Prompts, Chats, Settings |

---

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings > Preferences | Preferences page loads |
| 2 | Verify current theme is NOT Dark | Light or Project theme is active |
| 3 | Click on "Dark" theme option | Dark option is selected |
| 4 | Observe immediate UI color change | Background changes to dark colors |
| 5 | Verify sidebar background is dark | Sidebar uses dark background color |
| 6 | Verify main content area background is dark | Content area has dark background |
| 7 | Verify text is light colored for readability | Text contrasts well against dark background |
| 8 | Navigate to Agents page | Page loads with dark theme |
| 9 | Navigate to Prompts page | Page loads with dark theme |
| 10 | Navigate to Chats page | Page loads with dark theme |
| 11 | Verify cards and components use dark styling | All UI components follow dark theme |
| 12 | Verify buttons and interactive elements are visible | Buttons have appropriate contrast |

---

## Expected Final State

Dark theme is applied consistently across all pages with proper contrast between background and text elements.

---

## Pass/Fail Criteria

**Pass:**
- Dark background colors applied throughout
- Text remains readable with proper contrast
- All pages display consistent dark theme
- No components retain light theme styling
- Interactive elements are clearly visible

**Fail:**
- Background remains light after selection
- Text is unreadable (poor contrast)
- Inconsistent theming across pages
- Some components not styled for dark mode
