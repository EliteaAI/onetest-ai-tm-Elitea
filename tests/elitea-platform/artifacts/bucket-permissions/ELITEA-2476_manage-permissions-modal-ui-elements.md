---
id: ELITEA-2476
title: "Manage Permissions Modal UI Elements"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, bug-area:current-release-scope, eng:frontend, r-2.0.5, nfr:ui]
requirements: [EliteaAI/elitea_issues#5912]
---
# ELITEA-2476: Manage Permissions Modal UI Elements

**Module:** Artifacts · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the Manage Permissions modal displays all required UI elements according to the redesign specifications.

**Coverage:**
- AC3 from Story #5912: Permission Exceptions table displays required columns
- Default permissions section
- Exceptions table structure

## Preconditions

- User is logged in to {{base_url}} (Team project)
- User has permission to manage bucket access
- A bucket exists with at least 2 users in Exceptions list

## Test Data

- Team project: "Bugs & Features" or similar
- Bucket with existing permission exceptions

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts in a Team project | Artifacts page opens |
| 2 | Select a bucket with existing exceptions | Bucket content is displayed |
| 3 | Click context menu "Manage access" (3 dots next to bucket name in sidebar) | "Manage Permissions" modal opens |
| 4 | Verify modal header | Header shows "Manage Permissions" with close (X) button |
| 5 | Verify Default Permissions section | Shows info banner: "All users have read/write permissions by default." |
| 6 | Verify Exceptions section header | Shows "Exceptions – N" where N is the count of exceptions |
| 7 | Verify table columns | Columns: Checkbox, Name (sortable), Email (sortable), Permissions |
| 8 | Verify "+" button above table | Plus button is present for adding exceptions |
| 9 | Verify Edit (pencil) icon above table | Bulk edit action is available |
| 10 | Verify Search field presence | Search field is present |
| 11 | Verify row actions | Each row has Edit and Delete icons in Actions column |
| 12 | Verify scrolling | On leptop screen there is possibility to scroll modal. And if several users are added in Exceptions section there is scrolling inside section |

## Expected Final State

Modal displays all required UI elements: header, default permissions info, exceptions count, table with correct columns, action buttons, and scrolling.

## Pass/Fail Criteria

**Pass:**
- All UI elements are present as specified
- Table columns are: Checkbox, Name, Email, Permissions, (Actions)
- Default permissions info banner is displayed
- Exceptions count matches actual table rows

**Fail:**
- Missing UI elements
- Wrong column order or names
- Missing default permissions section
- Count mismatch with actual exceptions
