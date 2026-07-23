---
id: ELITEA-2477
title: "Empty State When No Permission Exceptions Exist"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, bug-area:current-release-scope, eng:frontend, r-2.0.5, nfr:ui]
requirements: [EliteaAI/elitea_issues#5912]
---
# ELITEA-2477: Empty State When No Permission Exceptions Exist

**Module:** Artifacts · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the empty state is correctly displayed when a bucket has no permission exceptions.

**Coverage:**
- AC4 from Story #5912: Empty state is displayed when a bucket has no permission exceptions

## Preconditions

- User is logged in to {{base_url}} (Team project)
- User has permission to manage bucket access
- A bucket exists with zero permission exceptions

## Test Data

- Team project with Admin role
- Bucket with no exceptions (newly created or all exceptions removed)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts in a Team project | Artifacts page opens |
| 2 | Select a bucket with no exceptions | Bucket content is displayed |
| 3 | Click context menu "Manage access" (3 dots next to bucket name in sidebar) | "Manage Permissions" modal opens |
| 4 | Verify Default Permissions section | Shows: "All users have read/write permissions by default." |
| 5 | Verify Exceptions header | Shows "Exceptions – 0" |
| 6 | Verify empty state illustration | Empty state illustration/icon is displayed |
| 7 | Verify empty state message | Message: "No exceptions added yet" |
| 8 | Verify helper text | Text: "All users have read/write permissions by default." |
| 9 | Verify CTA button | "Add Exceptions" button is displayed and clickable |
| 10 | Click "Add Exceptions" button | Add exception modal opens |

## Expected Final State

Empty state is displayed with illustration, message, helper text, and CTA button to add exceptions.

## Pass/Fail Criteria

**Pass:**
- Empty state illustration is visible
- "No exceptions added yet" message is displayed
- Helper text about default permissions is shown
- "Add Exceptions" CTA button is present and functional

**Fail:**
- Empty table is shown instead of empty state
- Missing illustration or message
- "Add Exceptions" button is missing or non-functional
