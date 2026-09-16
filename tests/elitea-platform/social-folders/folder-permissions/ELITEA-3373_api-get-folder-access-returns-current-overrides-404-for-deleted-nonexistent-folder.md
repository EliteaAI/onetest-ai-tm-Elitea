---
id: ELITEA-3373
title: "API: GET Folder Access Returns Current Overrides; 404 for Deleted/Nonexistent Folder"
priority: medium
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3373: API: GET Folder Access Returns Current Overrides; 404 for Deleted/Nonexistent Folder

**Module:** Social Folders · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that GET on the folder-access endpoint returns the current per-user overrides for an existing folder, and returns 404 for a deleted or nonexistent folder.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Admin user logged in to {{base_url}}
- A Team project with at least one entity folder that has no exceptions yet

## Test Data
- Endpoint: `GET {{base_url}}/api/v2/social/folder_access/prompt_lib/{project_id}/{folder_id}`
- Active folder_id: an existing folder in the Team project
- Deleted folder_id: a folder_id that was previously deleted
- Nonexistent folder_id: any ID that was never assigned

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | GET the active folder's access overrides (admin token) | `200`; body shape `{"ok": true, "folder_id": <id>, "overrides": [...]}` |
| 2 | GET using a deleted folder_id | `404` |
| 3 | GET using a folder_id that was never assigned | `404` |

## Expected Final State
No state change — this is a read-only endpoint.

## Pass/Fail Criteria
**Pass:**
- Active folder returns `200` with the documented shape
- Deleted and nonexistent folder IDs both return `404`

**Fail:**
- Active folder returns a non-`200` status
- Response shape differs from the documented shape
- A deleted or nonexistent folder returns anything other than `404`
