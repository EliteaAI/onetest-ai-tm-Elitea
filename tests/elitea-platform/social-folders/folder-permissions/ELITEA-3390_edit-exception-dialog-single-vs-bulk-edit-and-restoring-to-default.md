---
id: ELITEA-3390
title: "Edit Exception Dialog: Single vs. Bulk Edit, and Restoring to Default"
priority: critical
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3390: Edit Exception Dialog — Single vs. Bulk Edit, and Restoring to Default

**Module:** Social Folders · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Edit Exception dialog's single-row and bulk-edit behavior, its pre-ticking rules, Save gating, and that choosing Read/write (default) removes the exception(s).

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Logged in as Admin on a Team project
- Folder has at least 2 exceptions with **different** access levels (e.g. User A = `read_only`, User B = `no_access`)

## Test Data
- Permission choices in Edit exception: Read/write (default), Read-only, No access

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the per-row edit-exception icon for User A (`read_only`) | **Edit exception** dialog opens: "Select new folder permissions for <User A>.", Permissions dropdown pre-ticks **Read-only**; **Save** is disabled until a different value is chosen |
| 2 | Select **No access** | Save becomes enabled |
| 3 | Click **Cancel** | Dialog closes, no change persisted — User A's row still shows Read-only |
| 4 | Select both User A and User B rows (different current values), click **edit selected** | Dialog opens with plural title; Permissions dropdown shows **no** pre-ticked value (mixed selection) |
| 5 | Select **Read/write (default)** and Save | Both selected exceptions are removed; the **Exceptions** count decreases by 2 and both rows disappear from the table immediately after server success |

## Expected Final State
User A and User B both have no exception left (restored to RBAC-default access).

## Pass/Fail Criteria
**Pass:**
- Single edit pre-ticks the current value and gates Save on an actual change
- Bulk edit shows no pre-tick when values differ
- Choosing Read/write (default) deletes the exception(s) and the table updates immediately

**Fail:**
- Save is enabled without a change
- A pre-tick appears incorrectly in the mixed-selection bulk case
- Selecting Read/write (default) does not remove the exception
