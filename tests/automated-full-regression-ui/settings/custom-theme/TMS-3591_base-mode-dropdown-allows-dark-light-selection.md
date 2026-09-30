---
id: TMS-3591
title: "Base Mode dropdown allows selection of Dark Mode / Light Mode as foundation"
priority: high
type: functional
module: admin-portal/custom-theme
status: ready
execution_type: manual
tags: [feat:admin, feat:custom-theme, base-mode]
requirements: []
---

# TMS-3591: Base Mode dropdown allows selection of Dark Mode / Light Mode as foundation

**Module:** admin-portal/custom-theme · **Priority:** high · **Type:** functional

**Objective:** Verify that the Base Mode dropdown in Custom Theme configuration allows administrators to select either Dark Mode or Light Mode as the foundation for the custom theme.

---

## Preconditions

- User has Admin role with access to Admin Portal
- User is on Custom Theme configuration page
- No unsaved changes in progress

---

## Test Data

| Field | Value |
|-------|-------|
| Base Mode options | Dark Mode, Light Mode |
| Default selection | Dark Mode (typically) |

---

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin Portal > Features > Custom Theme | Custom Theme page loads |
| 2 | Locate "Base Mode" dropdown in the top toolbar | Base Mode dropdown is visible |
| 3 | Observe current Base Mode selection | Shows either "Dark Mode" or "Light Mode" |
| 4 | Click on Base Mode dropdown | Dropdown opens showing options |
| 5 | Verify "Dark Mode" option is available | Dark Mode option is listed |
| 6 | Verify "Light Mode" option is available | Light Mode option is listed |
| 7 | Select "Light Mode" (if Dark was selected, or vice versa) | Selection changes to chosen mode |
| 8 | Observe color section values | Color defaults may adjust based on base mode |
| 9 | Click "Save Changes" | Changes are saved |
| 10 | Refresh the page | Page reloads |
| 11 | Verify Base Mode selection persisted | Selected base mode is retained |
| 12 | Switch back to original Base Mode | Selection updates |
| 13 | Save and verify persistence | Change is saved correctly |

---

## Expected Final State

Base Mode dropdown allows switching between Dark Mode and Light Mode foundations, with selection persisting after save.

---

## Pass/Fail Criteria

**Pass:**
- Dropdown opens and shows both options
- Selection can be changed between modes
- Base mode selection saves correctly
- Selection persists after page refresh

**Fail:**
- Dropdown doesn't open or is disabled
- Options are missing
- Selection doesn't save
- Base mode resets after refresh
