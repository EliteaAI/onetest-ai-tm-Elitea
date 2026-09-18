---
id: ELITEA-3385
title: "Folder 3-Dot Menu Is Hidden for Any Role With a read_only Exception"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3385: Folder 3-Dot Menu Is Hidden for Any Role With a read_only Exception

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify that a `read_only` folder exception hides the folder's 3-dot menu for the affected user regardless of their base project role, while the folder itself remains visible and open-able.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Logged in to {{base_url}}/app/ as each role below in turn, on a Team project

## Test Data

| Entity type | Role | Exception on folder | Expected menu on hover |
|---|---|---|---|
| Agents / Pipelines / Toolkits / MCPs / Credentials | Viewer | none | menu (3 dots) not shown |
| Agents / Pipelines / Toolkits / MCPs / Credentials | Editor | none | menu shown |
| Agents / Pipelines / Toolkits / MCPs / Credentials | Admin | none | menu shown |
| any | Admin / Editor / Viewer | `read_only` | menu not shown, for **any** role including Admin — the folder itself is still visible and openable |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | For each in-scope entity type, log in as Viewer (no exception) and hover the folder | No 3-dot menu appears |
| 2 | Repeat as Editor and as Admin (no exception) | 3-dot menu appears for both |
| 3 | Apply a `read_only` exception to the folder for a test user, then hover as that user regardless of their base role | 3-dot menu does not appear, even for a user whose base role is Admin/Editor |
| 4 | Still as the `read_only` user, open the folder | Folder opens and its contents are browsable (read access is not blocked — only the menu/write actions are) |

## Expected Final State
No permanent state change — this case only asserts UI visibility.

## Pass/Fail Criteria
**Pass:**
- Menu visibility follows the table above for every entity type tested
- The folder itself remains open-able for the `read_only` user

**Fail:**
- The menu is visible where it should be hidden (or vice versa) for any role/entity-type combination
- The folder becomes unopenable for the `read_only` user
