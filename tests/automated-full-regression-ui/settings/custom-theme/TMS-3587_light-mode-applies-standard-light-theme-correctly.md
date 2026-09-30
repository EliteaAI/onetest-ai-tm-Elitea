---
id: TMS-3587
title: "Selecting Light mode applies standard light theme correctly"
priority: high
type: functional
module: settings/preferences
status: ready
execution_type: manual
tags: [feat:settings, theme, light-mode]
requirements: []
---

# TMS-3587: Selecting Light mode applies standard light theme correctly

**Module:** settings/preferences · **Priority:** high · **Type:** functional

**Objective:** Verify that selecting "Light" theme option applies the standard light color palette consistently across all UI components.

---

## Preconditions

- User is logged into ELITEA platform
- Current theme is set to Dark or Project (not Light)
- User has access to Settings > Preferences

---

## Test Data

| Field | Value |
|-------|-------|
| Expected background | Light (#ffffff or similar light shade) |
| Expected text | Dark colors for contrast |
| Test pages | Agents, Prompts, Chats, Settings |

---

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings > Preferences | Preferences page loads |
| 2 | Verify current theme is NOT Light | Dark or Project theme is active |
| 3 | Click on "Light" theme option | Light option is selected |
| 4 | Observe immediate UI color change | Background changes to light colors |
| 5 | Verify sidebar background is light | Sidebar uses light background color |
| 6 | Verify main content area background is light | Content area has light/white background |
| 7 | Verify text is dark colored for readability | Text contrasts well against light background |
| 8 | Navigate to Agents page | Page loads with light theme |
| 9 | Navigate to Prompts page | Page loads with light theme |
| 10 | Navigate to Chats page | Page loads with light theme |
| 11 | Verify cards and components use light styling | All UI components follow light theme |
| 12 | Verify buttons and interactive elements are visible | Buttons have appropriate contrast |

---

## Expected Final State

Light theme is applied consistently across all pages with proper contrast between background and text elements.

---

## Pass/Fail Criteria

**Pass:**
- Light/white background colors applied throughout
- Text remains readable with proper contrast
- All pages display consistent light theme
- No components retain dark theme styling
- Interactive elements are clearly visible

**Fail:**
- Background remains dark after selection
- Text is unreadable (poor contrast)
- Inconsistent theming across pages
- Some components not styled for light mode
