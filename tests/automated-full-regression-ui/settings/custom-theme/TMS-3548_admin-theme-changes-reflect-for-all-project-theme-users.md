---
id: TMS-3548
title: "Admin theme changes reflect for all users who select Project theme"
priority: high
type: functional
module: settings/custom-theme
status: ready
execution_type: manual
tags: [feat:custom-theme, multi-user, synchronization, end-to-end]
requirements: []
---

# TMS-3548: Admin theme changes reflect for all users who select Project theme

**Module:** settings/custom-theme · **Priority:** high · **Type:** functional

**Objective:** Verify that custom theme configuration set by an administrator is consistently applied to all users across the platform when they select the "Project" theme option, ensuring multi-user theme synchronization.

---

## Preconditions

- Admin user account with access to Admin Portal
- At least 2 additional non-admin user accounts (User A, User B)
- Users should be in different browsers or incognito sessions
- All users have access to the same project/environment

---

## Test Data

| Field | Value |
|-------|-------|
| Distinctive Primary Main color | #FF0000 (bright red) |
| Distinctive Secondary Main color | #00FF00 (bright green) |
| Test users | Admin, User A, User B |

---

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | **Admin session:** Log into Admin Portal | Admin Portal loads |
| 2 | Navigate to Features → Custom Theme | Custom Theme page loads |
| 3 | Set Primary Main to #FF0000 (bright red) | Color is set in picker/input |
| 4 | Set Secondary Main to #00FF00 (bright green) | Color is set in picker/input |
| 5 | Click "Save Changes" | Save completes with success notification |
| 6 | **User A session:** Open different browser/incognito | New browser session starts |
| 7 | Log in as User A | User A lands on platform |
| 8 | Navigate to Settings > Preferences | Preferences page loads |
| 9 | Select "Project" theme option | Project theme is selected |
| 10 | Observe UI colors | Bright red (#FF0000) accent colors are visible |
| 11 | Verify sidebar, buttons, and links reflect custom theme | UI elements show admin-configured colors |
| 12 | **User B session:** Open another browser/incognito | Third browser session starts |
| 13 | Log in as User B | User B lands on platform |
| 14 | Navigate to Settings > Preferences | Preferences page loads |
| 15 | Select "Project" theme option | Project theme is selected |
| 16 | Observe UI colors | Same bright red (#FF0000) accent colors visible |
| 17 | Compare User A and User B interfaces | Both users see identical custom theme colors |
| 18 | **Admin session:** Change Primary Main to #0000FF (blue) | Color updated in admin |
| 19 | Save changes | Save completes |
| 20 | **User A & B:** Refresh their pages | Pages reload |
| 21 | Verify both users now see blue (#0000FF) theme | Updated color reflects for both users |

---

## Expected Final State

All users who select "Project" theme see the same admin-configured custom colors, and when admin updates the theme, the changes propagate to all Project theme users upon their next page load.

---

## Pass/Fail Criteria

**Pass:**
- Admin can save custom theme configuration
- User A sees admin-configured colors when selecting Project theme
- User B sees identical colors to User A
- Theme updates by admin propagate to users on refresh
- Color consistency is maintained across all Project theme users

**Fail:**
- Users see different colors from admin configuration
- Users see different colors from each other
- Theme changes do not propagate to users
- Some UI components show inconsistent colors
- Custom theme only works for admin user
