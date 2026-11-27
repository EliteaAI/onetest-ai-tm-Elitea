---
id: ELITEA-4963
title: "Another user's Profile shows their own First login"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7490]
---

**Objective:** First login is per user: a second user sees their own value, not another user's.

## Preconditions

- Two users, **User A** and **User B**, with different first-login dates
- Note both users' `first_login` from `GET {{base_url}}/api/v2/auth/user/default` (each called with that user's session)

## Test Data

| Field | Value |
|-------|-------|
| Users | User A, User B |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as User B and open Settings → **Profile** | User ID shows User B's id; First login is directly above Last login |
| 2 | Compare First login with User B's `first_login` | Equal (in local time) |
| 3 | Compare with User A's First login | Different — User A's value is not shown |

## Expected Final State

Each user sees only their own First login.

## Pass/Fail Criteria

**Pass:**
- User B's Profile shows User B's `first_login`

**Fail:**
- User B sees User A's value, an empty value, or a value not matching the API
