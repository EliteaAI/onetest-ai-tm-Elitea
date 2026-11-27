---
id: ELITEA-4960
title: "Profile shows First login above Last login and it stays the same across project switches"
priority: critical
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7490]
---

**Objective:** Settings → Profile shows the persisted **First login** directly above **Last login**, unaffected by the selected project.

## Preconditions

- User is logged in to `{{base_url}}` and has logged in more than once
- The user is a member of at least two team projects

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{project_id}/settings/profile` |
| Oracle | `GET {{base_url}}/api/v2/auth/user/default` → `first_login`, `last_login` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Settings → **Profile** | Fields in order: Full name, Email, User ID, **First login**, Last login |
| 2 | Read First login and Last login | First login is a date and time formatted like **Last login** (browser locale and time zone, e.g. en-US `5/18/2026, 12:51:50 PM`); it differs from Last login |
| 3 | Call `GET {{base_url}}/api/v2/auth/user/default` | `first_login` (RFC 1123 GMT) is earlier than `last_login`; the UI First login equals `first_login` in local time |
| 4 | Compare Full name, Email, User ID, Last login with the API | All unchanged and equal to the API values |
| 5 | Switch the project in the sidebar to Team A, then Team B | First login and Last login stay exactly the same in the UI and in the API |

## Expected Final State

First login is shown per user, above Last login, and does not depend on the project.

## Pass/Fail Criteria

**Pass:**
- Field order is correct
- First login equals the API value and never changes on project switch

**Fail:**
- First login is missing, equals Last login, is placed elsewhere, or changes on project switch
