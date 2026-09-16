---
id: ELITEA-3376
title: "API: PUT/DELETE Reject Empty Array or Missing Required Key"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3376: API: PUT/DELETE Reject Empty Array or Missing Required Key

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify that PUT and DELETE on the folder-access endpoint reject requests with an empty array or a missing required key, without side effects.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Admin user logged in to {{base_url}}
- Target folder exists in a Team project

## Test Data

| # | Method | Body | Expected |
|---|---|---|---|
| 1 | PUT | `{"entries":[]}` | `400` — `min_length=1` |
| 2 | PUT | `{}` (no `entries` key) | `400` — `entries` required |
| 3 | DELETE | `{"user_ids":[]}` | `400` — `min_length=1` |
| 4 | DELETE | `{}` (no `user_ids` key) | `400` — `user_ids` required |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send each PUT/DELETE variant from the Test Data table | Every variant returns `400` |
| 2 | GET the folder's overrides after each attempt | Folder state unchanged |

## Expected Final State
No override rows are created, modified, or removed by any of the malformed requests.

## Pass/Fail Criteria
**Pass:**
- All 4 variants return `400`

**Fail:**
- Any variant is accepted (non-`400`)
- Any variant has a side effect on folder state
