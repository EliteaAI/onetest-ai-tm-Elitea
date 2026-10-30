---
id: ELITEA-1986
title: "Build with AI — Access Control (Role-Based Visibility)"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills]
requirements: []
---

# ELITEA-1986: Build with AI — Access Control (Role-Based Visibility)

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify that the "Build with AI" (Magic Wand) button is visible for admin and editor roles, but NOT visible for viewer role, ensuring role-based access control is correctly enforced.

---

## Preconditions

- The Elitea platform is accessible.
- Three user accounts exist with different roles: admin, editor, and viewer.
- The Skills page is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Admin role user | A valid user account with admin role |
| Editor role user | A valid user account with editor role |
| Viewer role user | A valid user account with viewer role |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as a user with admin role | Login is successful and the user is redirected to the platform home |
| 2 | Navigate to the Skills page and click "+ Skill" | The New Skill creation screen opens |
| 3 | Verify the "Build with AI" / Magic Wand button is visible on the New Skill creation screen | The "Build with AI" / Magic Wand button is displayed on the creation screen |
| 4 | Log out | User is logged out successfully |
| 5 | Log in as a user with editor role | Login is successful and the user is redirected to the platform home |
| 6 | Navigate to the Skills page and click "+ Skill" | The New Skill creation screen opens |
| 7 | Verify the "Build with AI" / Magic Wand button is visible for the editor role | The "Build with AI" / Magic Wand button is displayed for the editor role |
| 8 | Log out | User is logged out successfully |
| 9 | Log in as a user with viewer role | Login is successful and the user is redirected to the platform home |
| 10 | Navigate to the Skills page and click "+ Skill" (if accessible) | The New Skill creation screen opens (or access is restricted) |
| 11 | Verify the "Build with AI" / Magic Wand button is NOT displayed on the New Skill creation screen | The "Build with AI" / Magic Wand button is absent from the creation screen |
| 12 | Verify there is no way for a viewer to trigger the AI Skill Creator flow | No UI element enables the viewer to access the AI Skill Creator |

---

## Expected Final State

- Admin and editor roles can see the "Build with AI" button on the New Skill creation screen.
- Viewer role cannot see or access the "Build with AI" button, with no alternative trigger available.

---

## Pass/Fail Criteria

**Pass:**
- All assertions verified:
  - "Build with AI" button is visible for admin role
  - "Build with AI" button is visible for editor role
  - "Build with AI" button is NOT visible for viewer role
  - No alternative access method exists for viewer role

**Fail:**
- Any assertion fails:
  - Button is not visible for admin or editor role
  - Button is visible or accessible to viewer role

---

## Notes

**Source functional tests:** ELITEA-1986, ELITEA-1987

**Regression rationale:** Consolidated from 2 tests to verify role-based access control in a single flow covering all three roles (admin, editor, viewer), eliminating redundant login/navigation steps.

**Selected checkpoints:** Button visibility for admin, editor, and hidden for viewer; no alternative access method for viewer.
