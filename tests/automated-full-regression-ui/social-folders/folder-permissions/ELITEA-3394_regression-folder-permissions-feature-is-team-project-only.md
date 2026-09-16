---
id: ELITEA-3394
title: "[Regression] Folder-Permissions Feature Is Team-Project-Only"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6, regression]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3394: [Regression] Folder-Permissions Feature Is Team-Project-Only

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Regression confirmation that both the UI entry point and the underlying API scope folder-level permission exceptions to Team projects only.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Admin has access to both a Team project and a Private/personal project, each with at least one entity folder

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | On the Team project folder, open the 3-dot menu | **Manage permissions** is present |
| 2 | On the Private/personal project folder, open the 3-dot menu | **Manage permissions** is absent |
| 3 | PUT a folder exception directly against the Private/personal project's folder | Rejected (`400`/`403`) |

## Expected Final State
No override created on the Private/personal project's folder.

## Pass/Fail Criteria
**Pass:**
- The entry point and the API both scope the feature to Team projects only

**Fail:**
- The menu entry or the API accepts the operation outside a Team project
