---
id: ELITEA-3393
title: "[Regression] API: RBAC and Central Resolver Enforcement for Folder-Access Endpoints"
priority: critical
type: integration
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6, regression]
requirements: [EliteaAI/elitea_issues#6524, EliteaAI/elitea_issues#6558]
---
# ELITEA-3393: [Regression] API: RBAC and Central Resolver Enforcement for Folder-Access Endpoints

**Module:** Social Folders · **Priority:** Critical · **Type:** Integration

**Objective:** Regression consolidation of both enforcement layers — Viewer RBAC denial on the folder-access endpoints, and central-resolver denial of write operations under a read-only exception — with a strict no-partial-state-change check.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects
- Related defect #6558: false-success responses for denied write operations under a read-only exception

## Preconditions
- Tokens available for Admin, Editor, and Viewer on the same Team project; a folder with a `read_only` exception applied to a fourth test user

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call GET/PUT/DELETE on `folder_access` as Viewer | All three return `403` |
| 2 | Call GET/PUT/DELETE on `folder_access` as Editor and as Admin | All succeed (`200`) for both roles |
| 3 | As the `read_only`-excepted user, attempt rename/delete/move/create on the folder | Each returns `403`; no state change on any of them |
| 4 | As Admin, GET the folder after step 3 | Folder is byte-for-byte unchanged from before step 3 |

## Expected Final State
No unintended writes from any denied call; folder state fully intact.

## Pass/Fail Criteria
**Pass:**
- All denials are enforced server-side (`403`) with zero state change, for both the RBAC layer (Viewer) and the resolver layer (read-only exception)

**Fail:**
- Any denied call is permitted
- Any denied call produces a false-success (state unchanged but a success response/toast is returned) — tracked historically under #6558
