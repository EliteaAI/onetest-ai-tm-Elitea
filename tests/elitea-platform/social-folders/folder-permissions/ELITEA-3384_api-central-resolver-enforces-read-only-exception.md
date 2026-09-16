---
id: ELITEA-3384
title: "API: Central Resolver Enforces a Read-Only Exception Across Dependent Folder Operations"
priority: critical
type: integration
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524, EliteaAI/elitea_issues#6558]
---
# ELITEA-3384: API: Central Resolver Enforces a Read-Only Exception Across Dependent Folder Operations

**Module:** Social Folders · **Priority:** Critical · **Type:** Integration

**Objective:** Verify that a user with a `read_only` folder exception can read the folder but is blocked by the central permission resolver from any write operation (rename, delete, move, create), with no false-success responses.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects
- Related defect #6558: false-success responses for denied write operations under a read-only exception

## Preconditions
- A folder exists in a Team project
- A test user has a `read_only` exception on that folder
- A valid token for the test user is available

## Test Data

| # | Action as the read-only user | Endpoint (reference) | Expected |
|---|---|---|---|
| 1 | GET folder details | `GET .../social/folder/prompt_lib/{project_id}/{folder_id}` | `200` — read is allowed |
| 2 | Rename the folder | `PUT .../social/folder/prompt_lib/{project_id}/{folder_id}` | `403` |
| 3 | Delete the folder | `DELETE .../social/folder/prompt_lib/{project_id}/{folder_id}` | `403` |
| 4 | Move an entity into/out of the folder | `PUT .../social/move_to_folder/...` | `403` |
| 5 | Create a new entity inside the folder | (entity creation endpoint, folder param) | `403` or blocked at creation |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As the read-only user, GET the folder | `200` |
| 2 | As the read-only user, attempt rename, delete, move, and create (one at a time) against the same folder | Each of the 4 write operations returns `403` — none succeeds |
| 3 | As Admin, GET the folder afterward | Folder is unchanged — name, contents, and location are exactly as before step 2 |

## Expected Final State
The folder is unchanged by any of the attempted write operations; only the read succeeded.

## Pass/Fail Criteria
**Pass:**
- Read succeeds; all 4 write operations are rejected server-side with `403` and produce no state change

**Fail:**
- Any write operation returns a non-`403` success status
- The API/UI reports success but the underlying state does not actually change (false-success, tracked historically under #6558) — this is a fail, not a pass, even if no error is shown
