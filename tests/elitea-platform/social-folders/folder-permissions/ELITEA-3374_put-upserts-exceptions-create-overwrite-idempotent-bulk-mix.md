---
id: ELITEA-3374
title: "PUT Upserts Exceptions: Create, Overwrite, Idempotent Repeat, Bulk Mix of New + Existing"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3374: PUT Upserts Exceptions: Create, Overwrite, Idempotent Repeat, Bulk Mix of New + Existing

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify that PUT on the folder-access endpoint upserts per-user exceptions — creating new ones, overwriting existing ones without duplication, behaving idempotently on repeat calls, and correctly handling a bulk payload mixing new and existing users.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Admin user logged in to {{base_url}}
- Target folder has no pre-existing exceptions for the test users below

## Test Data
- Endpoint: `PUT {{base_url}}/api/v2/social/folder_access/prompt_lib/{project_id}/{folder_id}`
- User A, User B: active Team-project members

| Step variant | Body | Expected |
|---|---|---|
| Create | `{"entries":[{"user_id":A,"access_level":"read_only"}]}` | `200`, `updated:1` |
| Overwrite same user | `{"entries":[{"user_id":A,"access_level":"no_access"}]}` | `200`, `updated:1` — value overwritten, not duplicated |
| Idempotent repeat | same body sent twice in a row | second call still `200`, GET shows exactly one row for A |
| Bulk mix (new + existing) | `{"entries":[{"user_id":A,"access_level":"read_only"},{"user_id":B,"access_level":"no_access"}]}` | `200`, `updated:2` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | PUT to create an exception for User A as `read_only` | `200`, `updated:1` |
| 2 | GET the folder's overrides | Row for User A present with `access_level: "read_only"` |
| 3 | PUT again for User A with `access_level: "no_access"` | `200`, `updated:1` |
| 4 | GET the folder's overrides | Exactly one row for User A, now `access_level: "no_access"` (overwritten, not a second row) |
| 5 | PUT the same body from step 3 again | `200` — repeat call succeeds identically |
| 6 | GET the folder's overrides | Still exactly one row for User A — no duplicate created by the repeat call |
| 7 | PUT a bulk payload with User A (existing) and User B (new) in one call | `200`, `updated:2` |
| 8 | GET the folder's overrides | Rows present for both User A and User B with the values just set |

## Expected Final State
Folder has exactly one override row per user, reflecting the last value written for each.

## Pass/Fail Criteria
**Pass:**
- Every PUT returns `200` with the correct `updated` count
- Repeated writes upsert (never duplicate rows)
- The unique `(project_id, folder_id, user_id)` constraint holds

**Fail:**
- A duplicate row appears for the same user
- An overwrite fails
- A repeat call errors instead of upserting
