---
id: TMS-3595
title: "Save Changes button persists all custom theme modifications"
priority: high
type: functional
module: admin-portal/custom-theme
status: ready
execution_type: manual
tags: [feat:admin, feat:custom-theme, save, persistence]
requirements: []
---

# TMS-3595: Save Changes button persists all custom theme modifications

**Module:** admin-portal/custom-theme · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking Save Changes successfully persists all custom theme modifications including colors, logo, and base mode selection.

---

## Preconditions

- User has Admin role with access to Admin Portal
- User is on Custom Theme configuration page
- Starting with default or known state

---

## Test Data

| Field | Value |
|-------|-------|
| Test Primary Main | #E91E63 (pink) |
| Test Secondary Main | #9C27B0 (purple) |
| Test background color | #1E1E2E |

---

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin Portal > Features > Custom Theme | Custom Theme page loads |
| 2 | Note current values for Primary Main and Secondary Main | Current values recorded |
| 3 | Change Primary Main to #E91E63 | Color updates in UI |
| 4 | Change Secondary Main to #9C27B0 | Color updates in UI |
| 5 | Expand Background Colors and change one value | Background color updates |
| 6 | Locate "Save Changes" button | Button is visible (typically top-right) |
| 7 | Click "Save Changes" button | Button shows loading/saving state |
| 8 | Wait for save operation to complete | Loading indicator disappears |
| 9 | Verify success notification appears | Toast/notification confirms "Changes saved" or similar |
| 10 | Refresh the page (F5) | Page reloads completely |
| 11 | Verify Primary Main shows #E91E63 | Saved value persisted |
| 12 | Verify Secondary Main shows #9C27B0 | Saved value persisted |
| 13 | Expand Background Colors section | Section expands |
| 14 | Verify changed background color persisted | Modified value retained |
| 15 | Close browser and reopen Admin Portal | New session starts |
| 16 | Navigate to Custom Theme | Page loads |
| 17 | Verify all saved values are retained | All modifications persist across sessions |

---

## Expected Final State

All custom theme modifications are persisted after save and retained across page refreshes and browser sessions.

---

## Pass/Fail Criteria

**Pass:**
- Save Changes button is functional
- Loading indicator shown during save
- Success notification displayed
- All values persist after page refresh
- Values persist across browser sessions
- Multiple sections' changes saved together

**Fail:**
- Save button doesn't respond
- No feedback during save operation
- Values reset after refresh
- Some changes lost while others saved
- Error during save operation
