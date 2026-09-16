---
id: ELITEA-3386
title: "Folder Is Entirely Invisible to Any Role With a no_access Exception"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3386: Folder Is Entirely Invisible to Any Role With a no_access Exception

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify that a `no_access` folder exception removes the folder entirely from the affected user's folder list and makes it unreachable, distinct from the `read_only` case where the folder stays visible with only the menu hidden.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Logged in to {{base_url}}/app/ as a Team-project member, on a folder they can currently see

## Test Data

| Entity type | Role | Exception on folder | Expected folder-list behavior |
|---|---|---|---|
| any | Admin / Editor / Viewer | `no_access` | folder is not listed at all — distinct from the `read_only` case, where the folder stays visible but only the menu is hidden |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As Admin, browse the folder list for the in-scope entity type and confirm the target folder is present | Folder is visible |
| 2 | Apply a `no_access` exception to the folder for a test user, regardless of that user's base role | `200` on the PUT |
| 3 | Log in as that user and browse the same folder list | The folder does **not** appear anywhere in the list — not just menu-restricted, but absent entirely |
| 4 | As that user, attempt to open the folder directly (e.g. via a bookmarked/direct URL if applicable, or a direct API GET on the folder) | Folder is not reachable — treated as if it does not exist for this user |
| 5 | As Admin, confirm the folder still exists and is unaffected | Folder is still present and unchanged for Admin |

## Expected Final State
No permanent state change to the folder itself — this case only asserts UI/API visibility for the excepted user; the folder remains fully intact for users without the exception.

## Pass/Fail Criteria
**Pass:**
- The folder is completely absent from the `no_access` user's folder list and unreachable by direct access, while remaining normal for everyone else

**Fail:**
- The folder is still listed (even if grayed out or menu-restricted) for the `no_access` user
- The folder is reachable via direct access
