---
id: ELITEA-3381
title: "Folder Creation Is Scoped to Its Own Project"
priority: high
type: integration
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3381: Folder Creation Is Scoped to Its Own Project

**Module:** Social Folders · **Priority:** High · **Type:** Integration

**Objective:** Verify that an entity folder created in one project is not visible in, or reachable from, another project.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Admin user has access to at least two distinct projects (a Team project and another project, e.g. a Private/personal project)

## Test Data
- Project A: Team project (`project_id`)
- Project B: another project the user has access to (`personal_project_id`)
- Folder name: any unique name, e.g. `perm-scope-check`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new entity folder named `perm-scope-check` in Project A | Folder created successfully, visible in Project A's folder list |
| 2 | Open Project B and check its folder list for the same entity type | `perm-scope-check` does **not** appear in Project B's folder list |
| 3 | Attempt to fetch the new folder's details using Project B's `project_id` and the folder's ID | Request fails (`404`/`400`) — the folder does not resolve under a project it does not belong to |

## Expected Final State
The folder exists only under Project A; Project B has no reference to it.

## Pass/Fail Criteria
**Pass:**
- The folder is visible only in the project it was created in, and does not resolve under any other project

**Fail:**
- The folder appears in, or is reachable from, a project other than the one it was created in
