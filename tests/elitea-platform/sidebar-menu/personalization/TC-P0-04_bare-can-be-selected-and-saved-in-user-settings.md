---
id: TC-P0-04
title: "Verify Bare Can Be Selected and Saved in User Settings"
priority: critical
type: functional
module: sidebar-menu/personalization
status: ready
execution_type: manual
tags: [p0, bare-personality, user-settings, persistence, r-2.0.4, 5264]
requirements: [EliteaAI/elitea_issues#5264]
---
# TC-P0-04: Verify Bare Can Be Selected and Saved in User Settings

**Module:** Personalization · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that users can select the "Bare" personality option in User Settings and successfully save the selection, with proper persistence.

**Coverage:**
- "Bare" option can be clicked and selected
- Dropdown displays "Bare" as selected value
- Save operation completes successfully
- Selection persists after navigation
- API call succeeds with 200 OK status

## Preconditions

- User is logged into EliteaUI
- User is on the Personalization settings page
- Current personality is set to "Generic" (or any other personality)
- "Bare" option is visible in the dropdown

## Test Data

- User: Valid test user account
- Previous personality: Generic
- New personality: Bare

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open User Settings → Personalization. | Personalization page is displayed. |
| 2 | Click on "Default Personality" dropdown. | Dropdown expands showing all options. |
| 3 | Select "Bare" from the dropdown options. | "Bare" is highlighted on click. |
| 4 | Verify the dropdown now displays "Bare" as selected. | Dropdown closes and shows "Bare" as current value. |
| 5 | Observe checkmark appears next to "Bare" in dropdown (reopen to verify). | Checkmark is visible next to "Bare". |
| 6 | Click "Save" button (if explicit save is required). | Save button is clicked. |
| 7 | Wait for save confirmation/success message. | Success message or indicator appears. |
| 8 | Open browser Developer Tools → Network tab and check API response. | API call returns 200 OK status. |
| 9 | Navigate away from the Personalization page (e.g., to Chat). | Navigation successful. |
| 10 | Navigate back to User Settings → Personalization. | Personalization page loads. |
| 11 | Check the "Default Personality" dropdown value. | "Bare" is still selected (persisted). |

## Expected Final State

User's default personality is set to "Bare" and persisted in the database. Setting remains after navigation.

## Pass/Fail Criteria

**Pass:**
- "Bare" option can be clicked and selected
- Dropdown displays "Bare" after selection
- Save operation succeeds without errors
- Success message appears (if applicable)
- API call returns 200 OK
- After navigation, "Bare" remains selected

**Fail:**
- Cannot select "Bare" option
- Save operation fails or shows error
- API call returns error status
- Selection is not persisted after navigation
- Any JavaScript console errors
