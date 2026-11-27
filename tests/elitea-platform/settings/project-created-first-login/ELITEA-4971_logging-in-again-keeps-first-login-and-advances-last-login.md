---
id: ELITEA-4971
title: "Logging in again keeps First login and advances Last login"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7490]
---

**Objective:** A new interactive login updates Last login only; First login is never overwritten.

## Preconditions

- A user who has logged in before (First login and Last login are set)
- Note the user's current `first_login` and `last_login` from `GET {{base_url}}/api/v2/auth/user/default`

## Test Data

| Field | Value |
|-------|-------|
| Oracle | `GET {{base_url}}/api/v2/auth/user/default` |
| Note | Right after a login the API may return the old `last_login` for up to ~1 min; re-read until it changes |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log out, then log in again through the login form | The user lands in the app |
| 2 | Call `GET {{base_url}}/api/v2/auth/user/default` (repeat until `last_login` changes) | `first_login` is unchanged; `last_login` advanced to the time of this login |
| 3 | Open Settings → **Profile** | First login shows the unchanged value; Last login shows the new login time |

## Expected Final State

Only Last login moved; First login keeps the user's original first login.

## Pass/Fail Criteria

**Pass:**
- `first_login` identical before and after
- `last_login` equals the new login time in the API and the UI

**Fail:**
- First login changed to the new login time, or Last login did not update
