---
id: ELITEA-2478
title: "Add Exception Modal Functionality"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, bug-area:current-release-scope, eng:frontend, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5832, EliteaAI/elitea_issues#5912]
---
# ELITEA-2478: Add Exception Modal Functionality

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that users can add permission exceptions to a bucket via the Add Exception modal.

**Coverage:**
- AC4 from Story #5832: User can add Team project users to a bucket
- AC5 from Story #5912: User can add a permission exception via the Add exception modal
- AC6 from Story #5912: User can cancel adding an exception without changes

## Preconditions

- User is logged in to {{base_url}} (Team project)
- User has permission to manage bucket access
- Team project has at least 3 users
- A bucket exists (can have existing exceptions or none)

## Test Data

- Team project: "Bugs & Features"
- Users: At least 2 users to add as exceptions
- Bucket: Any bucket in the project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Manage Permissions modal for a bucket | Modal opens |
| 2 | Click "+" button (or "Add Exceptions" in empty state) | "Add exception" modal opens |
| 3 | Verify modal header | Header shows "Add exception" |
| 4 | Verify description text | Shows "Select users, then assign their bucket permissions." |
| 5 | Click on Users dropdown | Searchable dropdown opens |
| 6 | Type a partial user name in search | Dropdown filters to matching users |
| 7 | Verify only Team project users are shown | Only users from current Team project appear |
| 8 | Select User A | User A is added to selection |
| 9 | Select User B | User B is added to selection (multi-select works) |
| 10 | Verify Permission dropdown options | Options: "No access", "Read-only" |
| 11 | Select "Read-only" permission | Permission is selected |
| 12 | Click Cancel | Modal closes, no changes saved |
| 13 | Reopen Add exception modal | Modal opens with empty fields |
| 14 | Select User A and User B again | Users selected |
| 15 | Select "Read-only" permission | Permission selected |
| 16 | Click Save | Modal closes, success notification appears |
| 17 | Verify Exceptions table | User A and User B appear with "Read-only" permission |

## Expected Final State

Selected users are added to the Exceptions table with the assigned permission.

## Pass/Fail Criteria

**Pass:**
- Users dropdown shows only Team project members
- Multi-select works for users
- Permission dropdown has two options
- Cancel closes modal without saving
- Save adds users to exceptions table
- Success notification is displayed

**Fail:**
- Users from other projects are shown
- Cannot select multiple users
- Missing permission options
- Cancel saves changes
- Save doesn't add users to table
