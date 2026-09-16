---
id: ELITEA-3391
title: "[Regression] Manage Permissions Modal — View, Add, and Edit Exceptions"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6, regression]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3391: [Regression] Manage Permissions Modal — View, Add, and Edit Exceptions

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Regression consolidation of the Manage Permissions modal flow — empty state, adding exceptions, editing a single exception, and bulk-restoring to default — in one reversible run, mirroring the artifacts/bucket-permissions regression consolidation pattern.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Admin logged in on a Team project; target folder starts with zero exceptions; at least 2 other active project members available with no existing exception

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open **Manage permissions** on a folder with 0 exceptions | Empty state shown: **Exceptions – 0**, "No exceptions added yet", **+ add exception** visible |
| 2 | Click **+ add exception**, select 2 users, choose **Read-only**, Save | Dialog closes; **Exceptions – 2**; both rows appear with Read-only |
| 3 | Select one row, click its edit icon, change to **No access**, Save | Row updates to No access; count stays at 2 |
| 4 | Select both rows, click **edit selected**, choose **Read/write (default)**, Save | Both rows removed; **Exceptions – 0** again |

## Expected Final State
Folder returns to zero exceptions at the end of the flow (fully reversible run for repeatable regression execution).

## Pass/Fail Criteria
**Pass:**
- Each step's UI state matches exactly, and the modal returns to empty state at the end

**Fail:**
- Any step's count/row content is wrong
- The flow does not cleanly return to the empty state
