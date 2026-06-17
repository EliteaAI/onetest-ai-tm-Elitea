---
id: ELITEA-0260
title: "Navigation and UI Consistency — Theme and Sidebar"
priority: medium
type: functional
module: applications
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:apps, r-2.0.3, 4770]
requirements: [EliteaAI/elitea_issues#4770]
---
# ELITEA-0260: Navigation and UI Consistency — Theme and Sidebar

**Module:** Applications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify general navigation behavior, theme rendering, Configured chip updates, and sidebar highlight consistency.

**Coverage:**
- Active tab preserved on return navigation
- Configured chip updates after new app creation
- Light and dark mode rendering
- Sidebar Applications item active state

## Preconditions

- Logged in as a project member
- On the Applications page
- A project with no configured apps of at least one type (to test chip update)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Configured tab; navigate to another section (e.g., Agents); return to Applications | Configured tab is shown (last active tab preserved) |
| 2 | Note an app type that currently has no configured apps. Create a new app of that type. Return to Request App tab. | 'Configured' chip appears on that app type's card |
| 3 | Toggle to dark mode (settings icon in top bar) | Applications section renders correctly without visual artifacts in dark mode |
| 4 | Toggle back to light mode | Applications section renders correctly in light mode |
| 5 | While on the Applications page, observe the sidebar | 'Applications' sidebar item is visually highlighted/active |

## Expected Final State

'Applications' sidebar item is visually highlighted/active

## Pass/Fail Criteria

**Pass:**
- Tab preserved on return; chip updates after creation; both themes render correctly; sidebar highlighted

**Fail:**
- Wrong tab on return, chip not updated, rendering broken in either theme, or sidebar not highlighted
