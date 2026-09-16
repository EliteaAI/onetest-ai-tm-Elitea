---
id: ELITEA-3377
title: "PUT With Duplicate user_id in One Payload Applies the Last Entry"
priority: medium
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3377: PUT With Duplicate user_id in One Payload Applies the Last Entry

**Module:** Social Folders · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a PUT payload contains the same user_id twice with conflicting access levels, the last entry in the array wins and only one row is written.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Admin user logged in to {{base_url}}
- Target user has no pre-existing exception on the folder

## Test Data
- Endpoint: `PUT {{base_url}}/api/v2/social/folder_access/prompt_lib/{project_id}/{folder_id}`
- Body: `{"entries":[{"user_id":664,"access_level":"read_only"},{"user_id":664,"access_level":"no_access"}]}` (same user twice, conflicting values)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | PUT the body above | `200` — request is accepted |
| 2 | GET the folder's overrides | Exactly one row exists for the user, with `access_level: "no_access"` (the last entry in the array wins) |

## Expected Final State
One override row for the user, value = the last-specified `access_level`.

## Pass/Fail Criteria
**Pass:**
- Request succeeds, exactly one row is written, and it reflects the last entry in the array — this documents current accepted behavior; there is no spec requirement to reject duplicates

**Fail:**
- A duplicate row is created
- The request errors
- The first (not last) value wins
