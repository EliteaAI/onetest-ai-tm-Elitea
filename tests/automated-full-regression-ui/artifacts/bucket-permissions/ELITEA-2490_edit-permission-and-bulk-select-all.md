---
id: ELITEA-2490
title: "Edit Permission and Bulk Select All Functionality"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: [EliteaAI/elitea_issues#5832, EliteaAI/elitea_issues#5912]
---

# ELITEA-2490: Edit Permission and Bulk Select All Functionality

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify single edit permission flow, bulk select all checkbox functionality, and bulk edit operations. Setting "Read & Write" removes users from Exceptions table.

---

## Preconditions

- User A (Admin) is logged in to the Elitea platform (Team project)
- User B and User C exist in the Team project
- A test bucket "permissionstest" exists
- User B and User C have default permissions (not in Exceptions)

---

## Test Data

| Field | Value |
|-------|-------|
| Project | Team project (e.g., "Bugs & Features") |
| Bucket name | permissionstest |
| User A | Admin user |
| User B | Test user 1 |
| User C | Test user 2 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Login as User A (Admin) | Login successful |
| 2 | Navigate to Artifacts and open Manage Permissions for bucket | Modal opens |
| 3 | Add User B with "Read-only" permission | User B added |
| 4 | Add User C with "No access" permission | User C added |
| 5 | Verify Exceptions table shows 2 users | "Exceptions – 2" displayed |
| 6 | Click Edit (pencil) icon on User B's row | Edit modal opens |
| 7 | Verify current permission shows "Read-only" | Current permission pre-selected |
| 8 | Change permission to "No access" | Permission changed |
| 9 | Click Save | User B now shows "No access" |
| 10 | Click checkbox in table header (Select All) | Both User B and User C checkboxes selected |
| 11 | Verify both row checkboxes are checked | Both rows selected |
| 12 | Click checkbox in table header again (Deselect All) | Both checkboxes unchecked |
| 13 | Verify both row checkboxes are unchecked | Both rows deselected |
| 14 | Click Select All checkbox in header | Both rows selected |
| 15 | Click bulk Edit (pencil) icon above table | Bulk edit modal opens |
| 16 | Verify modal indicates 2 users selected | Shows selected count |
| 17 | Select "Read & Write" permission | Permission selected |
| 18 | Click Save | Modal closes |
| 19 | Verify both users are removed from Exceptions table | Users removed (returned to default) |

---

## Expected Final State

Single edit changes permission correctly. Select All checkbox works for both select and deselect. Bulk edit to "Read & Write" removes all users from Exceptions, showing empty state.

---

## Pass/Fail Criteria

**Pass:**
- Single edit updates permission correctly
- Select All checkbox selects all rows
- Clicking Select All again deselects all rows
- Bulk edit applies permission to all selected users
- "Read & Write" removes users from Exceptions table
- Empty state displayed when no exceptions remain

**Fail:**
- Single edit doesn't save
- Select All doesn't work
- Bulk edit fails or affects wrong users
- "Read & Write" doesn't remove users from Exceptions
