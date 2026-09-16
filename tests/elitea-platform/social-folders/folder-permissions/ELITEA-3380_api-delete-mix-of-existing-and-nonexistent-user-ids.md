---
id: ELITEA-3380
title: "API: DELETE With a Mix of Existing and Nonexistent user_ids"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3380: API: DELETE With a Mix of Existing and Nonexistent user_ids

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify that DELETE succeeds for the existing user_id in a batch even when other user_ids in the same batch do not exist as project members.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Admin user logged in to {{base_url}}
- User 659 has an existing exception on the folder; user_id `999999` does not exist as a member

## Test Data
- Endpoint: `DELETE {{base_url}}/api/v2/social/folder_access/prompt_lib/{project_id}/{folder_id}`
- Body: `{"user_ids":[659, 999999]}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | PUT to ensure user 659 has an exception | `200` |
| 2 | DELETE with `{"user_ids":[659, 999999]}` | `200` |
| 3 | GET the folder's overrides | User 659's exception is removed; the nonexistent `999999` entry is ignored without causing a failure of the whole request |

## Expected Final State
User 659 has no override row; no error surfaced for the nonexistent user in the same batch.

## Pass/Fail Criteria
**Pass:**
- The existing user's exception is deleted and the request as a whole succeeds despite one nonexistent ID in the batch

**Fail:**
- The whole request fails because of the nonexistent ID (blocking a legitimate deletion)
- The request silently does nothing
