---
id: ELITEA-3340
title: "Skill version comparison respects edit permissions and prevents unauthorized saves"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6304]
---

## Preconditions

- Admin user account with edit permissions
- View-only user account without edit permissions
- Skill exists with 2+ versions

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Admin User | user1@example.com (edit permissions) |
| View-Only User | user2@example.com (view-only permissions) |
| Test Skill | Skill with 2+ versions |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as Admin User (user1@example.com) | Login successful |
| 2 | Navigate to Test Skill details page | Skill page loads |
| 3 | Create 2+ versions for the Skill if not already present | Versions created successfully |
| 4 | Log out and log in as View-Only User (user2@example.com) | Login successful |
| 5 | Navigate to Test Skill details page | Skill page loads |
| 6 | Verify Compare Versions button is NOT visible in actions menu | Button is hidden (P0 check confirmed) |
| 7 | Attempt to access comparison modal via direct URL manipulation (if URL pattern known) | Access denied or modal fails to open |
| 8 | If modal somehow opens, verify Instructions field is disabled or read-only | Field is read-only or disabled |
| 9 | If modal somehow opens, verify Save buttons are hidden or disabled | Save buttons not present or disabled |
| 10 | If Save button is accessible, attempt to click it and save changes | Save fails with permission error message |
| 11 | Verify error message indicates lack of edit permissions | Message: "You do not have permission to edit this Skill" or similar |

## Expected Final State

View-only users cannot access Compare Versions button for Skills, and if modal is accessed, all edit operations are prevented with permission errors.

## Pass/Fail Criteria

**Pass:**
- Compare Versions button hidden for view-only users (P0 check)
- If modal accessed, Instructions field is disabled or read-only
- Save buttons hidden or disabled for view-only users
- Save attempts fail with clear permission error message

**Fail:**
- Compare Versions button visible to view-only users
- Instructions field is enabled for view-only users
- Save operations succeed for view-only users
- No error message or unclear error message
