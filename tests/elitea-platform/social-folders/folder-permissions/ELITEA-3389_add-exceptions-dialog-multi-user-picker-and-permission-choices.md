---
id: ELITEA-3389
title: "Add Exceptions Dialog: Multi-User Picker and Permission Choices"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3389: Add Exceptions Dialog — Multi-User Picker and Permission Choices

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify the Add Exceptions dialog's multi-user selection/deselection, its two-option Permissions field, and that users who already have an exception are excluded from the picker.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Logged in as Admin on a Team project
- At least 2 active Team-project members with no existing exception on the target folder

## Test Data
- URL: {{base_url}}/app/
- User 1, User 2: active members with no existing exception on the folder

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Manage Permissions, click **+ add exception** | **Add exceptions** dialog opens with copy "Select users, then restrict their folder permissions.", a **Users** search field, and a **Permissions** field |
| 2 | Click the Users field | "Search users..." placeholder and a scrollable dropdown of active Team-project members appears |
| 3 | Select User 1 from the dropdown | User 1 is added as a chip with a deselect (x) icon; the dropdown shows a tick next to User 1 |
| 4 | Select User 2 as well | Both users appear as chips; both are ticked in the dropdown |
| 5 | Click the x on User 1's chip | User 1 is removed from the selection and its tick clears in the dropdown |
| 6 | Open the Permissions dropdown | Only two choices are offered: **Read-only** and **No access** (no "Read/write" option here) |
| 7 | Select **Read-only** and save with User 2 still selected | Exception created for User 2 with `read_only`; dialog closes; **Exceptions** count in the parent modal increments |
| 8 | Re-open **+ add exception** and open the Users dropdown | User 2 (who now has an exception) does not appear in the selectable list |

## Expected Final State
User 2 has a `read_only` exception on the folder; User 1 has none.

## Pass/Fail Criteria
**Pass:**
- Multi-select, deselect, and the two-option Permissions field all behave as described
- Users who already have an exception are excluded from the picker
- Save persists correctly

**Fail:**
- Any selection/deselection is inconsistent
- A third permission option appears
- A user with an existing exception is still selectable
