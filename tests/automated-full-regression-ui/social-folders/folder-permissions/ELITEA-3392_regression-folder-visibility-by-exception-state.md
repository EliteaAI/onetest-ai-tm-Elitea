---
id: ELITEA-3392
title: "[Regression] Folder Visibility by Exception State: Read-Only Hides Menu, No-Access Hides Folder"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6, regression]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3392: [Regression] Folder Visibility by Exception State — Read-Only Hides Menu, No-Access Hides Folder

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Regression consolidation confirming the two distinct visibility outcomes for the two exception levels, with cleanup restoring default access at the end.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Admin logged in on a Team project; two test users available (User A, User B), neither with an existing exception on the target folder

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Apply a `read_only` exception for User A on the folder; log in as User A | Folder is visible and openable in the folder list; 3-dot menu does not appear on hover |
| 2 | Apply a `no_access` exception for User B on the folder; log in as User B | Folder does not appear in the folder list at all |
| 3 | As Admin, remove both exceptions | Folder list and menu behavior return to normal (default RBAC) for both users |

## Expected Final State
Neither User A nor User B has an exception at the end of the run.

## Pass/Fail Criteria
**Pass:**
- Read-only produces "visible, no menu"; no-access produces "not listed"; both are distinguishable outcomes, and cleanup restores default state

**Fail:**
- Either exception state produces the wrong visibility outcome
- Cleanup fails to fully restore default access
