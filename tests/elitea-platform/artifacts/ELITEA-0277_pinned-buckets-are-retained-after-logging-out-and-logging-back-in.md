---
id: ELITEA-0277
title: "Pinned buckets are retained after logging out and logging back in"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, r-2.0.3, 4180]
requirements: [EliteaAI/elitea_issues#4180]
---
# ELITEA-0277: Pinned buckets are retained after logging out and logging back in

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that pin preferences are stored per user account and survive a full logout/login cycle, not just a page refresh.

**Coverage:**
- Pinned buckets are stored per user account (not browser session)
- Same pinned buckets are restored after logout and re-login
- No additional unintended buckets become pinned after re-login
- Pin state is not shared with or affected by other users

## Preconditions

- Logged in to ELITEA ({{base_url}}
- At least 2 buckets available to pin
- User credentials are known for re-login

## Test Data

- Buckets to pin: any 2 available buckets; note their names before logout
- Same user credentials required for re-login

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the left sidebar. | Bucket sidebar is visible. |
| 2 | Pin 2 buckets via ⋮ → 'Pin to top'. | Both buckets appear at the top with 📌 icons. |
| 3 | Note the exact names of the pinned buckets. | Names recorded. |
| 4 | Log out from ELITEA (user menu → Logout). | User is logged out; redirected to login page. |
| 5 | Log back in with the same user credentials. | Login succeeds; user is redirected to the main platform. |
| 6 | Navigate to Artifacts. | Artifacts page and bucket sidebar load. |
| 7 | Observe the bucket sidebar. | Both previously pinned buckets are at the top with 📌 icons; no other buckets have been inadvertently pinned. |

## Expected Final State

Both previously pinned buckets are at the top with 📌 icons; no other buckets have been inadvertently pinned.

## Pass/Fail Criteria

**Pass:**
- Same pinned buckets present and at the top after logout/re-login
- Pin state is user-account-specific and fully restored
- No additional unintended buckets are pinned

**Fail:**
- Pinned buckets are not restored after re-login
- Pin state is lost on logout
- Additional unintended buckets appear pinned
