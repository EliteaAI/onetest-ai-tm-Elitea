---
id: ELITEA-3383
title: "Authorization: Viewer Is Denied Folder-Permission Management (GET/PUT/DELETE); Editor and Admin Are Both Permitted"
priority: critical
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3383: Authorization — Viewer Is Denied Folder-Permission Management (GET/PUT/DELETE); Editor and Admin Are Both Permitted

**Module:** Social Folders · **Priority:** Critical · **Type:** Functional

**Objective:** Verify RBAC enforcement on the folder-access endpoints: Viewer is denied on GET, PUT, and DELETE; Editor and Admin are both permitted on all three.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Valid Bearer tokens available for a user with Admin role, a user with Editor role, and a user with Viewer role, all on the same Team project

## Test Data

| Method | Role | Expected |
|---|---|---|
| GET | Admin | `200` |
| GET | Editor | `200` |
| GET | Viewer | `403` |
| PUT | Admin | `200` |
| PUT | Editor | `200` |
| PUT | Viewer | `403` |
| DELETE | Admin | `200` |
| DELETE | Editor | `200` |
| DELETE | Viewer | `403` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call GET/PUT/DELETE on the folder-access endpoint with the Admin token | All three calls succeed (`200`) |
| 2 | Call GET/PUT/DELETE with the Editor token | All three calls succeed (`200`) |
| 3 | Call GET/PUT/DELETE with the Viewer token, **including GET** | All three methods are denied (`403`) for Viewer — this was explicitly re-confirmed for GET, not assumed by analogy with PUT/DELETE |
| 4 | Repeat the Admin GET call once more as a control check | Still `200` — confirms Admin access was not affected by the preceding negative tests |

## Expected Final State
No unintended data changes from the Viewer calls (all rejected before mutation); Admin/Editor calls behave per their normal PUT/DELETE effects.

## Pass/Fail Criteria
**Pass:**
- Viewer is denied on all three methods (GET included)
- Admin and Editor are both permitted on all three methods

**Fail:**
- Viewer is permitted on any call
- Admin/Editor is unexpectedly denied
