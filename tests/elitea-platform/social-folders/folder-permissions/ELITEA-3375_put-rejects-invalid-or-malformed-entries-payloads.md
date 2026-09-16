---
id: ELITEA-3375
title: "PUT Rejects Invalid or Malformed Entries Payloads"
priority: high
type: functional
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3375: PUT Rejects Invalid or Malformed Entries Payloads

**Module:** Social Folders · **Priority:** High · **Type:** Functional

**Objective:** Verify that PUT on the folder-access endpoint rejects entries with invalid enum values, missing/mistyped fields, out-of-range values, and oversized arrays, and that no partial state is written.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Admin user logged in to {{base_url}}
- Target folder exists in a Team project

## Test Data

| # | Body | Expected |
|---|---|---|
| 1 | `{"entries":[{"user_id":659,"access_level":"read_write"}]}` | `400` — `read_write` is not a valid enum value (only `read_only`/`no_access` accepted) |
| 2 | `{"entries":[{"user_id":659,"access_level":"admin"}]}` | `400` — invalid enum |
| 3 | `{"entries":[{"user_id":659,"access_level":""}]}` | `400` |
| 4 | `{"entries":[{"user_id":659}]}` (missing `access_level`) | `400` |
| 5 | `{"entries":[{"access_level":"read_only"}]}` (missing `user_id`) | `400` |
| 6 | `{"entries":[{"user_id":"abc","access_level":"read_only"}]}` (wrong type) | `400` |
| 7 | `{"entries":[{"user_id":-1,"access_level":"read_only"}]}` (`user_id` must be `gt=0`) | `400` — validation error, **not** a 5xx |
| 8 | `{"entries":[<201 objects>]}` (over 200 entries) | `400` — `max_length=200` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send PUT with each body variant from the Test Data table, one at a time, against a folder in a known-clean state | Every variant returns `400` |
| 2 | GET the folder's overrides after each attempt | No override was written from any rejected request |

## Expected Final State
No override rows are created or modified by any of the invalid payloads.

## Pass/Fail Criteria
**Pass:**
- All 8 variants return `400` and leave folder state unchanged

**Fail:**
- Any variant returns `200` (silently accepted invalid data)
- Variant 7 (negative `user_id`) returns a `5xx` instead of `400` — known anomaly seen during exploratory testing (actual result was `503`); re-verify this specific row and treat a repeat `5xx` as a regression, not a pass
