---
id: ELITEA-3378
title: "PUT Bulk Write Is All-or-Nothing (One Invalid Entry Fails the Whole Batch)"
priority: critical
type: integration
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3378: PUT Bulk Write Is All-or-Nothing (One Invalid Entry Fails the Whole Batch)

**Module:** Social Folders · **Priority:** Critical · **Type:** Integration

**Objective:** Verify that a bulk PUT with a mix of valid and invalid entries is rejected as a whole, and that none of the valid entries are partially applied.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Admin user logged in to {{base_url}}
- Neither test user has a pre-existing exception on the folder

## Test Data
- Endpoint: `PUT {{base_url}}/api/v2/social/folder_access/prompt_lib/{project_id}/{folder_id}`
- Body: `{"entries":[{"user_id":659,"access_level":"read_only"},{"user_id":664,"access_level":"no_access"},{"user_id":611,"access_level":"read_write"}]}` — 2 valid entries + 1 invalid enum

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | PUT the mixed valid/invalid batch above | `400` — whole request rejected because one entry is invalid |
| 2 | GET the folder's overrides | Neither the 659 nor the 664 entries were written — the valid entries in the failed batch are **not** partially applied |

## Expected Final State
No override rows exist for any user referenced in the failed batch.

## Pass/Fail Criteria
**Pass:**
- Batch is rejected with `400` and GET confirms zero partial writes

**Fail:**
- Batch returns `200`
- GET shows that 659 and/or 664 were written despite the batch failing (partial write / non-atomic behavior)
