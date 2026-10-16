---
id: ELITEA-4077
title: "Admin can access Custom Theme page under Features menu in Admin Portal"
priority: high
type: functional
module: admin-portal/features
status: ready
execution_type: manual
tags: [feat:admin, feat:custom-theme, navigation]
requirements: []
---

# ELITEA-4077: Admin can access Custom Theme page under Features menu in Admin Portal

**Module:** admin-portal/features · **Priority:** high · **Type:** functional

**Objective:** Verify that administrators can navigate to and access the Custom Theme configuration page within the Admin Portal's Features section.

---

## Preconditions

- User has Admin role with access to Admin Portal
- Admin Portal is accessible at the environment URL
- Custom Theme feature is enabled

---

## Test Data

| Field | Value |
|-------|-------|
| Admin Portal URL | dev.elitea.ai/admin/app/features#custom_theme |
| Navigation path | Features > Custom Theme |

---

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin Portal login | Admin Portal login page loads |
| 2 | Log in with admin credentials | Admin Portal dashboard loads |
| 3 | Locate "Features" in the left sidebar | Features menu item is visible |
| 4 | Click on "Features" | Features submenu expands or Features page loads |
| 5 | Locate "Custom Theme" option in Features menu | Custom Theme option is visible in the list |
| 6 | Click on "Custom Theme" | Custom Theme configuration page loads |
| 7 | Verify page header/title indicates Custom Theme | Page title confirms Custom Theme section |
| 8 | Verify description text is present | Text: "Customize the platform appearance with your brand colors and logo" or similar |
| 9 | Verify Base Mode dropdown is present | Base Mode selector is visible |
| 10 | Verify Import/Export JSON buttons are present | Import JSON and Export JSON buttons visible |
| 11 | Verify Save Changes button is present | Save Changes button is visible |
| 12 | Verify color configuration sections are present | Platform Logo, Primary Colors, Background Colors, etc. sections visible |

---

## Expected Final State

Admin successfully navigates to Custom Theme page which displays all configuration options for customizing platform appearance.

---

## Pass/Fail Criteria

**Pass:**
- Features menu is accessible
- Custom Theme option is visible and clickable
- Custom Theme page loads without errors
- All expected UI elements are present (Base Mode, colors, logo, buttons)

**Fail:**
- Features menu not accessible to admin
- Custom Theme option missing
- Page fails to load or shows error
- Configuration elements are missing
