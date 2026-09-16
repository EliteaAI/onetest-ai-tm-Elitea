---
id: ELITEA-3379
title: "DELETE Removes an Exception and Restores Default Access; Idempotent When Already Absent"
priority: critical
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3379: DELETE Removes an Exception and Restores Default Access; Idempotent When Already Absent

**Module:** Social Folders · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that DELETE removes a folder-access exception entirely (restoring default RBAC access), and that deleting an already-absent exception is a harmless no-op.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Admin user logged in to {{base_url}}

## Test Data
- Endpoint: `DELETE {{base_url}}/api/v2/social/folder_access/prompt_lib/{project_id}/{folder_id}`
- Body: `{"user_ids":[659]}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | PUT to create a `read_only` exception for user 659 | `200` |
| 2 | GET the folder's overrides | Row for 659 present with `access_level: "read_only"` |
| 3 | DELETE with `{"user_ids":[659]}` | `200` |
| 4 | GET the folder's overrides | Row for 659 is **entirely gone** from `overrides` — this is how default access is restored, not represented by any `access_level` value |
| 5 | DELETE again with `{"user_ids":[659]}` (user already has no exception) | `200`, no-op — does not error just because nothing existed to delete |

## Expected Final State
No override row exists for user 659; the user has RBAC-default access to the folder.

## Pass/Fail Criteria
**Pass:**
- DELETE removes the row entirely (not a tombstone/empty value)
- A repeat DELETE on an already-clean state is a harmless `200` no-op

**Fail:**
- The row persists with some placeholder value after DELETE
- A repeat DELETE errors
