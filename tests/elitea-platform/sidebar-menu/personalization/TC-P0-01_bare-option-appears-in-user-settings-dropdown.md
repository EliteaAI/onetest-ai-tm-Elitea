---
id: TC-P0-01
title: "Verify Bare Option Appears in User Settings Dropdown"
priority: critical
type: functional
module: sidebar-menu/personalization
status: ready
execution_type: manual
tags: [p0, bare-personality, user-settings, r-2.0.4, 5264]
requirements: [EliteaAI/elitea_issues#5264]
---
# TC-P0-01: Verify Bare Option Appears in User Settings Dropdown

**Module:** Personalization · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "Bare" personality option appears in the User Settings → Personalization → Default Personality dropdown and is properly visible and accessible to users.

**Coverage:**
- "Bare" option is visible in the dropdown list
- "Bare" displays correct description text
- "Bare" appears in alphabetical order
- Option is selectable and not disabled

## Preconditions

- User is logged into EliteaUI
- User has valid authentication token
- User has access to Settings page
- "Bare" personality type has been added to the system

## Test Data

- User: Valid test user account
- Expected dropdown options: Generic, QA, Nerdy, Quirky, Cynical, None, Bare
- Expected description: "No Elitea identity — only your instructions plus tool-required guidance"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the main application dashboard. | Dashboard loads successfully. |
| 2 | Click on "Settings" in the left sidebar navigation. | Settings page opens. |
| 3 | Click on "Personalization" in the settings menu. | Personalization section is displayed. |
| 4 | Locate the "Default Personality" section under "GENERAL". | "Default Personality" dropdown is visible. |
| 5 | Click on the "Default Personality" dropdown to expand it. | Dropdown expands showing all personality options. |
| 6 | Scroll through the dropdown options to locate "Bare". | All personality options are visible. |
| 7 | Verify "Bare" option is present in the list. | "Bare" option is visible in dropdown. |
| 8 | Check the description text below "Bare". | Description reads: "No Elitea identity — only your instructions plus tool-required guidance" |
| 9 | Verify "Bare" appears after "Cynical" and before "Generic" (alphabetical order). | "Bare" is positioned correctly in alphabetical order. |
| 10 | Check that "Bare" is not disabled or grayed out. | "Bare" option is interactive and selectable. |

## Expected Final State

"Bare" personality option is visible, properly described, alphabetically ordered, and selectable in the User Settings dropdown.

## Pass/Fail Criteria

**Pass:**
- "Bare" option appears in the Default Personality dropdown
- Description text is correct and matches specification
- "Bare" is positioned in correct alphabetical order
- Option is enabled and selectable
- No UI glitches or rendering issues

**Fail:**
- "Bare" option is missing from dropdown
- Description is incorrect, missing, or improperly formatted
- "Bare" is not in alphabetical order
- Option is disabled or grayed out
- UI rendering issues present
