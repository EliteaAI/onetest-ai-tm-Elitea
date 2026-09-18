---
id: ELITEA-3388
title: "Manage Permissions Modal: Populated State (Table, Search, Select-All, Bulk Actions)"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3388: Manage Permissions Modal — Populated State (Table, Search, Select-All, Bulk Actions)

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify the Manage Permissions modal's table content, exception count, search filtering, and select-all/per-row selection behavior when a folder has existing exceptions.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Logged in as Admin on a Team project
- Target folder has at least 2 existing exceptions (e.g. one `read_only`, one `no_access`) — the exact count is a precondition, not a fixed number; the modal heading must reflect however many exist

## Test Data
- Exception 1: generic user A (e.g. "Test User One" / `user1@example.com`) — `read_only`
- Exception 2: generic user B (e.g. "Test User Two" / `user2@example.com`) — `no_access`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open **Manage permissions** for the folder | Heading shows **Exceptions – N**, where N is the number of exceptions actually present as a precondition (N=2 in this run); a search box, **+ add exception**, and **edit selected** control are visible |
| 2 | Inspect the table | Columns: select checkbox, Name, Email, Permissions, per-row edit-exception icon. Rows show User A's name/email with "Read-only" and User B's name/email with "No access" |
| 3 | Type a name/email fragment in search that matches only one row | Only the matching row is shown |
| 4 | Clear the search | Both rows return |
| 5 | Click the select-all checkbox | Both rows become selected; **edit selected** becomes enabled |
| 6 | Click the per-row checkbox for just one row | Only that row is selected |

## Expected Final State
No data changes — this case is display/interaction only.

## Pass/Fail Criteria
**Pass:**
- The **Exceptions – N** count matches the actual number of precondition exceptions
- Table content, search filtering, and select-all/per-row selection all behave as described

**Fail:**
- The count does not match the actual number of exceptions
- Any column/value is wrong
- Search does not filter correctly
- Selection controls do not toggle as expected
