---
id: ELITEA-0003
title: "Select Bare personality and verify persistence after page reload"
priority: critical
type: functional
module: personalization
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5264]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Default Personality is currently set to "Generic" or any other value

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/personalization` |
| Initial Value | Generic |
| New Value | Bare |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Personalization | Personalization page loads |
| 2 | Click on "Default Personality" dropdown | Dropdown expands |
| 3 | Select "Bare" from the dropdown | Dropdown closes and displays "Bare" as selected value |
| 4 | Observe if there's an explicit save button or auto-save indicator | Save mechanism is visible (button or auto-save message) |
| 5 | If save button exists, click it; if auto-save, wait 2 seconds | Settings are saved successfully |
| 6 | Press F5 to reload the page | Page reloads completely |
| 7 | Navigate back to Personalization settings | Personalization page loads |
| 8 | Verify "Default Personality" field shows "Bare" | Selection is persisted |
| 9 | Open browser DevTools → Console | Console is open |
| 10 | Verify no JavaScript errors in console | No errors related to personality selection |

## Expected Final State

Default Personality is set to "Bare" and persists after page reload with no console errors.

## Pass/Fail Criteria

**Pass:**
- "Bare" is successfully selected
- Selection persists after page refresh
- No console errors or warnings
- Save mechanism works correctly

**Fail:**
- Selection reverts to previous value after reload
- Console shows errors
- Save fails or shows error message
