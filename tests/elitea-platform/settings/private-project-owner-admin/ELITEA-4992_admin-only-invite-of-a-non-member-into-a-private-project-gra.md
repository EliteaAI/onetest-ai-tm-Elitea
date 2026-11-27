---
id: ELITEA-4992
title: "Admin-only invite of a non-member into a private project grants no Admin"
priority: medium
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [feat:roles-permissions, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7507]
---

**Objective:** Adding a non-member to a private project with only the `admin` role doesn't give them Admin, and the response, the membership and the UI agree on what happened.

## Preconditions

- User A (owner of P-A) and User B are available. Accounts and API calls: [test-data/private-project-owner-admin](../../../../test-data/private-project-owner-admin/README.md)
- User B is not a member of P-A. Note the "Teammates: N" count on P-A's Settings → General

## Test Data

| Field | Value |
|-------|-------|
| Request | `POST {{base_url}}/api/v2/admin/users/default/{P-A id}` `{"emails": ["<B email>"], "roles": ["admin"]}` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, send the request and note the response | Recorded (see Notes) |
| 2 | Call `GET admin/users/default/{P-A id}` | B is not a member, or a member without `admin`. User A still holds `admin` |
| 3 | Reload P-A's Settings → General | "Teammates" matches step 2 (unchanged if B wasn't added, +1 if B was) |
| 4 | If B was added, remove B | B is not a member of P-A |

## Expected Final State

User A is the only Admin of P-A; B is not a member.

## Pass/Fail Criteria

**Pass:**
- B never holds `admin` in P-A; User A keeps it
- The Teammates count matches the membership

**Fail:**
- B holds `admin`, or the count and the membership disagree

## Notes

Observed on DEV 2026-11-27: the response is 200 `[{"msg": "user ... added to project ...", "status": "ok"}]`, but nobody is added. The guard works, but the success message is false. Record it; whether this should be a 4xx or a warning is a product decision, so it doesn't fail this case.
