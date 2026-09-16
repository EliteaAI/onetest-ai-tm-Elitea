---
id: ELITEA-3382
title: "Feature Is Team-Project-Only; Rejected for Private/Personal Project"
priority: critical
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3382: Feature Is Team-Project-Only; Rejected for Private/Personal Project

**Module:** Social Folders · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that folder-level permission exceptions are supported only in Team projects, both at the API level and via the UI entry point.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Admin user has access to a Private/personal project with at least one entity folder

## Test Data
- Endpoint: `PUT {{base_url}}/api/v2/social/folder_access/prompt_lib/{personal_project_id}/{folder_id_in_that_project}`
- Body: `{"entries":[{"user_id":659,"access_level":"read_only"}]}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | PUT a folder exception targeting a folder that belongs to a Private/personal project | Request is rejected (`400`/`403`) — folder exceptions are not supported outside Team projects |
| 2 | Confirm via the UI that **Manage permissions** does not appear in the folder menu for this project | Menu entry is absent in Private/personal projects |

## Expected Final State
No override is created; the Private project's folder behavior is unaffected.

## Pass/Fail Criteria
**Pass:**
- The API rejects the request and the UI hides the entry point for non-Team projects

**Fail:**
- The API accepts the exception for a non-Team project
- The UI still shows **Manage permissions**
